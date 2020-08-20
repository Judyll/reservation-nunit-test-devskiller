# reservation-nunit-test-devskiller
This is a Reservation app with NUnit Test

Implement following validation rules:
            
(idea is to check all and give customer full information, not to stop after first fail - therefore enum with [Flags] Attribute is returned)

* newReservation.From must be the same day as newReservation.To. If it isn't, set result |= ValidationResult.MoreThanOneDay

* newReservation.From obviously can't be >= newReservation.To. If it is, set result |= ValidationResult.ToBeforeFrom

* whole newReservation must be included inside working hours: 8-18 (it can't start before 8 and must finish at 18 at the very latest).

* If it's not met, set result |= ValidationResult.OutsideWorkingHours
            
* newReservation must last 3 hours at most. If it's not, set result |= ValidationResult.TooLong
            
* newReservation obviously cannot be in conflict (same hallNumber and overlapping hours) with any existing reservation. If it is, set result |= ValidationResult.Conflicting. Use _queryAll to get all extisting reservations.

* check if newReservation.LectureHallNumber points at existing lecture hall. If it's not, set result |= ValidationResult.HallDoesNotExist. Use _queryAllLectureHalls to get all extisting lecture halls
            
* check if newReservation.LecturerId points at existing lecturer. If it's not, set result |= ValidationResult.LecturerDoesNotExist. Use _queryAllLecturers to get all extisting lecturers

Remember ! Check ALL validation rules and set result with appropriate enum flag described above.
Note that for reservation dates, we take into account only date and an hour, minutes and seconds don't matter.
