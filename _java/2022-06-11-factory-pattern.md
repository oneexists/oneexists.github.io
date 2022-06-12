---
layout: post
title: "Implementing the Factory Pattern"
author: skylar_lynner
---

Some details are omitted for brevity.

### AppUser Factory

```
public interface AppUserFactory {
	AppUser create(String name, String username, String password);
}
```

### Factory Implementation

```
public class AppUserFactoryImpl implements AppUserFactory {
	@Override
	public AppUser create(String name, String username, String password) {
		return new AppUser(name, username, password);
	}
}
```

### Factory Provider

```
public class AppUserProvider {
	public static AppUserFactory getFactory() {
		return new AppUserFactoryImpl();
	}
}
```

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
