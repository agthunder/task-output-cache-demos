# OUTDATED - USE THE BUILD CACHE GUIDE

The documentation found here is outdated and will not be updated any more.
For up to date documentation have a look at current documentation about the [build cache](https://docs.gradle.org/current/userguide/build_cache.html) and on [using the build cache](https://guides.gradle.org/using-build-cache/). 


# WARNING: OLD INFORMATION
```
 _______  __   __  _______  ______   _______  _______  _______  ______  
|       ||  | |  ||       ||      | |   _   ||       ||       ||      | 
|   _   ||  | |  ||_     _||  _    ||  |_|  ||_     _||    ___||  _    |
|  | |  ||  |_|  |  |   |  | | |   ||       |  |   |  |   |___ | | |   |
|  |_|  ||       |  |   |  | |_|   ||       |  |   |  |    ___|| |_|   |
|       ||       |  |   |  |       ||   _   |  |   |  |   |___ |       |
|_______||_______|  |___|  |______| |__| |__|  |___|  |_______||______| 
```

## Task Output Cache

Task output caching is a new kind of cache mechanism in Gradle that aims to save time by, instead of executing a task, reusing results produced by previous executions of the same task with matching inputs. Reusing results can happen between builds happening in the same project, or in two different projects on the same computer, or even between builds running on different computers. Task output caching does not define the service to be used to store and retreive the results. Instead it only specifies a simple protocol that can be implemented to adopt different kinds of existing services as cache backends.

### How to try the feature?

We now have [sample scenarios](samples) you can try out. You can try using the [local cache backend](samples/01-simple-local-caching) the easiest, while using an [HTTP cache backend](samples/03-use-http-backend) gives you the most versatility.

If you want to try the cache on your own projects, you can do so by:

1. Update the wrapper in your Java project to the latest [Gradle release](https://gradle.org/install/).
2. Run builds with `./gradlew --build-cache` with the local cache backend (or you can also use the HTTP backend set up in the [HTTP backend sample](samples/03-use-http-backend)).

#### How to make existing tasks cacheable?

We have [some documentation on that](docs/making-custom-tasks-cacheable.md).

#### How to diagnose task caching?

See [here](docs/diagnosing-task-cache.md) how to get additional diagnostics for your build.

#### Local cache backend directory configuration

Task output caching currently works with a local directory as the cache backend. There is no eviction policy, so entries once added to the cache stay there indefinitely. The cache directory by default is in `$GRADLE_HOME/task-cache`. It can be moved to a different location by supplying `-Dorg.gradle.cache.tasks.directory=...`. This can be useful when setting up automated tests for example.
