requests-threads
================

This repo contains a Requests session that returns awaitable Twisted
Deferreds instead of response objects.

Examples
--------

Example Usage (using Async/Await)::

	from requests_threads import AsyncSession

	session = AsyncSession()

	async def _main():
	    rs = []
	    for _ in range(100):
	        rs.append(await session.get('http://httpbin.org/get'))
	    print(rs)

	if __name__ == '__main__':
	    session.run(_main)

Example Usage (using Twisted)::

	from twisted.internet.defer import inlineCallbacks
	from twisted.internet.task import react
	import requests

	session = requests.AsyncSession()

	@inlineCallbacks
	def main(reactor):
	    responses = []
	    for i in range(100):
	        responses.append(session.get('http://httpbin.org/get'))

	    for response in responses:
	        r = yield response
	        print(r)

	if __name__ == '__main__':
	    react(main)

Each request is sent via a new thread, automatically. This works fine for basic
use cases.

This is a preview of the true asyncronous API we have panned for Requests
that is currently *in the works*, but requires a lot of development time.

✨🍰✨

Installation
------------

::

    $ pipenv install requests-threads
    ✨🍰✨