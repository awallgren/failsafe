# 1.0.2

### Bug Fixes

* Fixed #75 - Incorrect future completion when a fallback is present.

# 1.0.1

### Changes

* `FailsafeException` now has public constructors, for easier mocking and testing.

# 1.0.0

### API Changes

* Failsafe will now only throw `FailsafeException` when an execution fails with a checked `Exception`. See [issue #66](https://github.com/jhalterman/failsafe/issues/66) for details.

# 0.9.5

### Bug Fixes

* Fixed #59 - Classloading issue on Java 6/7.

# 0.9.4

### Bug Fixes

* Fixed #63 - Proper handling of thread interrupts during synchronous execution delays.
* Fixed #54 - Added hashCode and equals implementations to Duration.

# 0.9.3

### New Features

* Added OSGi support.
* `FailsafeFutuer.cancel` calls completion handlers. `.get` after cancel throws `CancellationException`.

### Bug Fixes

* Fixed #52 - FailsafeFuture.cancel not working as expected.
* Fixed #55 - Fallback always called for asynchronous executions.

### API Changes

* `CircuitBreakerOpenException` now extends `FailsafeException`.

# 0.9.2

### New Features

* Various fallback and listener API additions and improvements

# 0.9.1

### New Features

* Added support for retry delay [jitter](https://github.com/jhalterman/failsafe#retry-policies).

# 0.9.0

### New Features

* Added support for [fallbacks](https://github.com/jhalterman/failsafe#fallbacks).

### Bug Fixes

* Fixed issue #36 - Failed attempt listener not always called on completion.
* Fixed issue #34 - CircuitBreaker should default to closed state.

# 0.8.3

### Bug Fixes

* Fixed #33 - `CircuitBreaker` not decrementing currentExections when under load

# 0.8.2

### New Features

* Added support for `onRetriesExceeded` listeners.
* `RetryPolicy` can be extended (it's no longer marked as final)

### Bug Fixes

* Abort should not call failure listeners.

# 0.8.1

### New Features

* Simplified listeners API.
* Added support for failure listeners via `Failsafe.with(...).onFailure(e -> {})`.
* Added `onAbort` listeners.
* Added additional async listeners.
* `RetryPolicy` and `CircuitBreaker` now support multiple configuration rules. Ex: `new RetryPolicy().retryWhen(null).retryWhen("")`. If any rule matches then the policy is matched.

### API Changes

* Added top level support for listener registration via `Failsafe.with(...).onXxx`. The `Listeners` class is now only meant for Java 6 and 7 usage via method overrides.
* Removed listener registration from `Listeners` class.
* Removed `AsyncListeners` class. 
* Removed listener registration from `FailsafeFuture` class.

# 0.8.0

### New Features

* Added support for circuit breakers

### API Changes

* Project renamed from Recurrent to Failsafe

# 0.7.1

### Bug Fixes

* Added better support for scheduling failure handling
* Fixed RetryPolicy failure assignability checking

### API Changes

* Invocation APIs were renamed to Execution to better align with the `java.util.concurrent` naming.
* `InvocationStats.getAttemptCount()` was renamed to `ExecutionStats.getExecutions()`

# 0.7.0

### New Features

* Added additional contextual callable and runnable support

### API Changes

* Changed to a new API entry point: `Recurrent.with`.
* Added `.with` for configuring listeners.


# 0.6.0

### New Features

* Added `RetryPolicy.abortOn`, `abortWhen` and `abortIf` methods to abort retries when matched.

### API Changes

* `RetryPolicy.retryWhen` was renamed to `retryIf` for retrying if a `Predicate` is matched.
* `RetryPolicy.retryFor` was renamed to `retryWhen` for retrying when a result is matched.
* `Scheduler` and `Schedulers` were moved to `net.jodah.recurrent.util.concurrent`.

# 0.5.0

### New Features

* Added support for synchronous and asynchronous event listeners
* Added support for `CheckedRunnable`

### API Changes

* The `Recurrent.run` methods now require a `CheckedRunnable` rather than `Runnable`. This allows Recurrent to be used on code that throws checked exceptions without having to wrap the code in try/catch blocks.
* The synchronous `Recurrent.run` and `Recurrent.get` methods will throw a `RecurrentException` if a failure occurs and the retry policy is exceeded.

# 0.4.0

### New Features

* Added better support for invocation tracking

### API Changes

* New Invocation and `AsyncInvocation` APIs

# 0.3.3

### New Features

* Add `Scheduler` API
* Make `RetryPolicy` copyable

### Behavior Changes

* Require `ContextualCallable` and `ContextualRunnable` to be manually retried
* Add support for checking multiple retry policy conditions

### API Changes

* Make ContextualRunnable throw Exception

# 0.3.2

### New Features

* Add support for retrying when an invocation result matches a policy

# 0.3.1

### New Features

* Added support for seprate retry tracking.

# 0.3.0

* Initial Release