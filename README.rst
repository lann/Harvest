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

Example::

	import sys
	from harvest import Harvest, HarvestError
	from datetime import datetime, timedelta
	import time

	URI = 'https://foo.harvestapp.com'
	EMAIL = 'foo@bar.com'
	PASS = 'xxxxxx'

	h = Harvest(URI,EMAIL,PASS)

	while True:
		total = 0
		dose = 0

		start = datetime.today().replace( hour=0, minute=0, second=0 )
		end = start + timedelta(1)
		try:
			for user in h.users():
				for entry in user.entries( start, end ):
					total += entry.hours

			text = '%0.02f' % total
			print text

		except HarvestError:
			print 'Retrying in 5 minutes...'

		time.sleep(300)

Example::

	for project in h.projects:
		print project
		print project.client
		for assignment in project.task_assignments:
			print '\t',assignment
		for entry in project.entries:
			print '\t',entry
			print '\t\ttask:',entry.task

Example::

	for client in h.clients:
		print client
		for contact in client.contacts:
			print '\t',contact
