# Enums

In Orange, Enums are algebreic data types. They can be given extra values to store.

The most simple `enum` is just a list of names:

```
enum Status {
	PENDING,
	RUNNING,
	FINISHED,
	ERRORED
}
```

The enum values are functions and can be passed as such. In this case, their type is `() -> Status`. However, since they aren't storing any values, they do not have to be called like functions to be used. Orange will accept both of the following:

```
var myStatus: Status = Status.FINISHED
var myStatus: Status = Status.FINISHED()
```

If we wanted to give `Status` some values to store:

```
enum Status {
	PENDING(Date),
	RUNNING(Date),
	FINISHED(Date),
	ERRORED(Date, string)
}

var myStatus = Status.PENDING(Date.now)
```

Since all the components of this version of `Status` store values, we can't use the parameter-less default version of creating it.

Like tuples, the components can also be named:

```
enum Status {
	PENDING(since: Date),
	RUNNING(since: Date),
	FINISHED(on: Date),
	ERRORED(on: Date, error: string)
}

var myStatus = Status.PENDING(Date.now)

// or:
var myStatus = Status.PENDING(since: Date.now)
```

To be able to decouple and do condition checks on the enums with values, we must use the [Switch](switch.md) block.
