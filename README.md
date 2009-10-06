Shlip (Sharing Clips)
=====================

Design Notes
------------
* A single device will be used in each participating copy of Live.

* [live.observer] watches all clips on the track containing the device.

* When a clip is added (or deleted?), the device will broadcast a message containing
  all the meta data needed to reconstruct the clip.
  (see below for format)

* Any copies of the device that receive the broadcasted message will look for a track
  matching the received track name

* If the track name exists on the receiving side, then the clip will be reconstructed
  at the indicated clip index in that track (this currently requires that a clip 
  already exists in the slot since the Live API does not yet allow creating a clip)


Message format:
--------------------
	track {name}
	index {clip_index}
	name {clip_name}
	length {clip_length}
	notes {number_of_notes}
	note {pitch} {starttime} {duration} {velocity} {is_deactivated}
	note ...
	note ...
	....
	done 


Message format details
----------------------
- the track name is the name of the track containing the device (the one being observed)
- pitch and velocity are standard midi values 0-127
- clip_length, starttime and duration are in terms of beats (float value)
