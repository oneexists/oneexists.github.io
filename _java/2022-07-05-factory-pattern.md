---
layout: post
title: "Implementing the Factory Pattern"
author: skylar_lynner
---

### Advantages of using the Factory Pattern:
- It eliminates coupling during creation of the AppUser by providing an interface
  to interact with.
- Creating a factory interface allows for the implementation class to define 
  object creation details.

This pattern allows for the separation of concerns by removing the need to provide 
the creation details related to creating a user, creating flexibility in the 
details related to creating a user. The separation allows for easily defining 
the implementation details of how users are created, opening up possibilities of 
using different class implementations for different types of users or different 
strategies to create users in different ways. 

One way of applying this pattern would allow for the reuse of the same AppUser, 
but defining a second method in the interface that provides a mechanism for 
creating an AppUser with Admin roles rather than User roles, providing the 
central location to specify how AppUser objects are created rather than defining 
these details directly in the AppUser constructors.

This pattern is especially helpful for situations where the AppUser class is an
interface for creating different types of users. The factory can define the 
creation of the AppUser while leaving the specifics to the implmentation details
to define how the different types of users can be created.

### Defining the Factory and Testing its Use 
First, the interface can be created to define the parameters needed to create a 
new user. In this example, the user is created by providing a name, username 
and password, so the interface defines this interaction.

#### AppUser Factory Interface

```
public interface AppUserFactory {
	AppUser create(String name, String username, String password);
}
```

The next step would be to create an implementation class to define how the user 
will be created. Our implementation class specifies that the creation involves 
using the defined parameters to create a new AppUser object. 

#### AppUser Factory Implementation Class

```
public class AppUserFactoryImpl implements AppUserFactory {
	@Override
	public AppUser create(String name, String username, String password) {
		return new AppUser(name, username, password);
	}
}
```

Now that the definition of how a user is created has been written, the next step 
would be to define a class for the application to use to access this factory. 
This implementation looks like how many singleton objects are created, but instead
of returning the singleton instance, it returns the implementation of the factory.

### Factory Provider Class

```
public class AppUserProvider {
	public static AppUserFactory getFactory() {
		return new AppUserFactoryImpl();
	}
}
```

Creating a class with a static method that returns the factory will accomplish 
this task. At this point, the creation of the user has been defined and the 
application now has a way to access this factory, so the creation logic can be 
separated from the AppUser object and replaced with the usage of the factory.

To provide assurance that the factory works, a quick test can be made. To build 
this test, the factory is created in the setUp() method to provide the creation 
of the user before any tests. Then a test can be built to verify that the user 
created with the factory is able to be successfully saved by the service. This 
test ensures that the saving mechanism of the service successfully asks the 
repository to save the AppUser. The repository is mocked in this test to isolate 
the testing to the service layer to verify that the service responds to the 
request as expected.

### Save AppUser Test with Factory Provider

```
import static org.assertj.core.api.Assertions.assertThat;

@SpringBootTest
class AppUserServiceTests {
	AppUser testAppUser;

	@Mock
	private AppUserRepository repository;
	@Mock
	private PasswordEncoder passwordEncoder;
	private AppUserService service;

	@BeforeEach
	void setUp() throws Exception {
		service = new AppUserServiceImpl(repository, passwordEncoder);
		AppUserFactory userFactory = AppUserProvider.getFactory();

		testAppUser = userFactory.create("Jesse Jackson", "user", "magnets");
	}

	@AfterEach
	void tearDown() throws Exception {
		testAppUser = null;
	}

	@Test
	void testSaveUser() {
		service.saveUser(testAppUser);
		ArgumentCaptor<AppUser> appUserArgCaptor = ArgumentCaptor.forClass(AppUser.class);
		verify(repository).save(appUserArgCaptor.capture());
		assertThat(appUserArgCaptor.getValue()).isEqualTo(testAppUser);
	}
}
```

### Resources
To find some quick information about the Factory Pattern, there is general information
and quick examples on the [Wikipedia page](https://en.wikipedia.org/wiki/Factory_method_pattern) 
for the pattern. To find more in depth information about this pattern and others, 
the best resource would be to reference the [Design Patterns](https://www.goodreads.com/book/show/85009.Design_Patterns) 
textbook by the Gang of Four.
