===================
Harvest API
===================

Example::

	from datetime import datetime, timedelta
	from harvest import Harvest

	h = Harvest( 'https://foo.harvestapp.com', 'foo@bar.com', 'mypassword' )
	user = h.find_user( 'John', 'Doe' )
	if user:
		print "The user ID = %d' % user.id

		start = datetime.today()
		end = start + timedelta(7)

		total = 0
		for entry in user.entries( start, end ):
			total += entry.hours

		print 'Total hours worked = %f' % total
