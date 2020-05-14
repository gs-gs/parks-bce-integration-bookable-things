Design
======

This is the logical model,
from the perspective of the Parks System.

.. uml::

   class BookableThing
   class Park {
     e.g. ANBG
   }
   Park o-- BookableThing

   class DeliveryOrg {
     e.g. ANBG Education Officers
   }
   DeliveryOrg o-- BookableThing
   
   class Booking {
     status
     start_time
     end_time
   }
   BookableThing o-- Booking
   class Availability {
     start_time
     end_time
   }
   BookableThing o-- Availability
   class Agent {
     e.g. BCE
   }
   Agent o-- Booking
   class Customer {
     e.g. Hogwarts
   }
   Customer o-- Booking


Bookable Thing
   The thing which is booked... Deliberately generic.

Park
   Parks Australia is a coalition of separate organisations called Parks...

Delivery Org
   Somebody is responsible for delivering the Bookable Thing.
   In the current project, this is a small team within Parks Australia
   (the education officers for ANBG)
   however in theory it could also be a commercial tour operator.
   The Parks Staff who confirm or deny pending bookings are in this org.
   They are also the BCE systen users that manage bookings directly in BCE
   and configure bookable education experiences in BCE.

Availability
   This is a slice of time when
   a particular the Bookable Thing
   may be booked.
   The Delivery Org members create these
   (using some kind of calendar interface).
   when they plan to have the bookable thing available.
   They are negated by bookings.

Agent
   In the current project, the only Agent is BCE.
   Agents make tentative Bookings,
   which may be confirmed or denied by the Delivery Org.

Customer
   The party on who's behalf the booking is made.
   i.e. the School (or teacher).

Booking
   An apointment to use the Bookable Thing.
   Made by an Agent
   on behalf of a Customer.

Statechart of a booking:

.. uml::

   [*] --> pending
   pending --> denied
   denied --> [*]
   pending --> accepted
   accepted --> completed
   completed --> [*]
   pending --> cancelled
   cancelled --> [*]
   accepted --> cancelled