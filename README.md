

## Developing

### Setting up a development environment
Requirements:
* Some sort of shell environment
* A reasonably recent version of Docker (>= 17.06, ideally 17.12)
* docker-compose (= 1.18)
* Basic familiarity with Docker keywords: image, container (https://docs.docker.com/get-started/#docker-concepts)

Setup:
1. Clone the repo 
2. Navigate to the root of the working copy, where the README file is.
3. Copy `default.env` file to `.env` in root.
4. Uncomment the `COMPOSE_FILE=` line in `.env` to enable mounting of working copy code into the containers.
4. Build a Docker image containing our backend code: `docker-compose build contract_observer`
5. Create the database and migrate it to the latest schema: `docker-compose run contract_observer alembic upgrade head`
6. Run the backend systems: `docker-compose up`. You can shut everything down with Ctrl+C at any time.

Tips:
* There are multiple containers running our backend code: `contract_observer`, `etherdelta_observer`, `websocket_server`.
* Running `docker-compose build <service-name>` for any of the above builds the same image.
* `docker-compose build contract_observer` builds an image, copying the code and installing Python libraries in our dependencies.
  You have to rebuild any time the dependencies change; however, in development, code in the working copy is mounted into the container,
  so it's enough to restart the container (with `docker-compose restart <service-name>`) to apply changes for a given service.
* You can inspect the list of currently running containers with `docker-compose ps`.

## Contributors
* [Arseniy Ivanov](https://github.com/freeatnet)
* [Jonathon Dunford](https://github.com/JonathonDunford)
* [Tanvir Rahaman](https://github.com/bitbd83)

## License

Copyright (C) 2018

    This program is free software: you can redistribute it and/or modify
    it under the terms of the GNU Affero General Public License as published
    by the Free Software Foundation, either version 3 of the License, or
    (at your option) any later version.

    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU Affero General Public License for more details.

    You should have received a copy of the GNU Affero General Public License
    along with this program.  If not, see <http://www.gnu.org/licenses/>.

