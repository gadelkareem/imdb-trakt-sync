[![sync](https://github.com/cecobask/imdb-trakt-sync/actions/workflows/sync.yaml/badge.svg)](https://github.com/cecobask/imdb-trakt-sync/actions/workflows/sync.yaml)
[![quality](https://github.com/cecobask/imdb-trakt-sync/actions/workflows/quality.yaml/badge.svg)](https://github.com/cecobask/imdb-trakt-sync/actions/workflows/quality.yaml)
[![codecov](https://codecov.io/gh/cecobask/imdb-trakt-sync/graph/badge.svg)](https://codecov.io/gh/cecobask/imdb-trakt-sync)
# imdb-trakt-sync
Command line application that can sync [IMDb](https://www.imdb.com/) and [Trakt](https://trakt.tv/dashboard) user data - watchlist, lists, ratings and optionally history.  
To achieve its goals the application is using the [Trakt API](https://trakt.docs.apiary.io/) and web scraping.  
Keep in mind that this application is performing one-way sync from IMDb to Trakt. This means that any changes made on IMDb will be reflected on Trakt, but not the other way around.


# Usage 
The application can be setup to run automatically, based on a custom schedule (_default: once every 3 hours_) using 
`GitHub Actions` or locally on your machine. Follow the relevant section below, based on how you want to use the application. 


## Run the application using GitHub Actions
1. [Fork the repository](https://github.com/cecobask/imdb-trakt-sync/fork) to your account
2. Create a [Trakt App](https://trakt.tv/oauth/applications). Use **urn:ietf:wg:oauth:2.0:oob** as redirect uri
3. Configure the application:
   - Open your fork repository on GitHub
   - Create an individual repository secret for each [configuration](config.yaml) parameter: `Settings` > `Secrets and variables` > `Actions` > `New repository secret`
   - The secret names should match the configuration parameter paths (delimited by underscore). For example, to configure your Trakt email, the secret name should be **TRAKT_EMAIL**
4. Allow GitHub Actions on your fork repository: `Settings` > `Actions` > `General` > `Allow all actions and reusable workflows`
5. Enable the **sync** workflow: `Actions` > `Workflows` > `sync` > `Enable workflow`
6. Run the **sync** workflow manually: `Actions` > `Workflows` > `sync` > `Run workflow`
7. From now on, GitHub Actions will automatically trigger the **sync** workflow

## Run the application locally
1. Clone the repository to your machine
2. [Create a Trakt API application](https://trakt.tv/oauth/applications). Give it a name and use `urn:ietf:wg:oauth:2.0:oob` as redirect uri. The rest 
of the fields can be left empty
3. Replace the parameter values in the [configuration](config.yaml) file or set up environment variables that
match the configuration paths, prefixed with `ITS_`. For example, to configure your Trakt email, the environment variable name should be `ITS_TRAKT_EMAIL`
4. Make sure you have Go installed on your machine. If you do not have it, [this is how you can install it](https://go.dev/doc/install)
5. Open a terminal window in the repository folder and run the application using the command `make sync`
