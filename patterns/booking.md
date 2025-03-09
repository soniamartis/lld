# Booking Pattern in LLD

- Requires user, entity to be booked and a class to link user to entity
- In reality a user can book several entities, eg user books n rooms, or user books n seats in movie/ flight booking
- Payment systems are always provided with diff modes of payment like cash/ credit card
- Booking and payment are separate, we can create a booking first with status as created and on payment, we can update status of that booking. On failure , we retry n times and then release the booking
- It will be nice to use some state machine here for transitioning states of the booking, so that it doesnt go into an inconsistent state
- Define some admin methods as well like adding entities, regisering users etc
- Bookings/ reservations require some uniqueId generators, where we can use several methods like UUID.randomUUID() or prefix + Intant.now() + atomicInteger.incrementAndGet()
