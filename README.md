# QKRT Software Onboarding Site

## Installation Prerequisites

Please follow to the steps below corresponding to your computer's operating system:

<details>
    <summary>Windows 10/11</summary>

1.  Download RubyInstaller with Devkit

    > [Ruby+Devkit 3.4.6-1 (x64)](https://github.com/oneclick/rubyinstaller2/releases/download/RubyInstaller-3.4.6-1/rubyinstaller-devkit-3.4.6-1-x64.exe)

    Make sure to check the box that adds Ruby executables to `PATH`.

    Verify that you have successfully installed Ruby 3.x by opening a new terminal and running:

    ```sh
    ruby -v
    ```

    You should see "Ruby" followed by a version number starting with `3.x`. For example:

    ```txt
    Ruby 3.4.5 [platform info...]
    ```

2.  Install `bundler` using `gem`

    ```sh
    gem install bundler
    ```

</details>

<details>
  <summary>macOS</summary>

1.  Download and Install Homebrew using the following command:

    ```sh
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    ```

    Verify that you have successfully installed homebrew using the following command:

    ```sh
    brew -v
    ```

2.  Use `brew` to download and install Ruby 3.x

    ```sh
    brew install ruby
    ```

    By default, macOS comes installed with Ruby 2.x which is too old. Add Homebrew's installation of Ruby to your `PATH` so that it overrides the system default version of Ruby.

    ```sh
    echo "export PATH=\"/opt/homebrew/opt/ruby/bin:$PATH\"" >> ~/.zprofile
    source ~/.zprofile
    ```

    Verify that you have successfully installed and are using Ruby 3.x by opening a new terminal and running:

    ```sh
    ruby -v
    ```

    You should see "Ruby" followed by a version number starting with `3.x`. For example:

    ```txt
    Ruby 3.4.5 [platform info...]
    ```

</details>

## Running the Website

### Cloning the Repository

Use `git` to clone this repository.

```sh
git clone https://github.com/qkrt-rm/onboarding.git
cd onboarding
```

### Install Dependencies

Install the Ruby gems (dependencies) listed in the project's Gemfile using the following command:

```sh
bundle install
```

### Run the Site Locally

To run the site locally on your machine, use the following command:

```sh
bundle exec jekyll serve --livereload
```

You should see the following output (or something similar):

```txt
Configuration file: /Users/hunter/dev/onboarding/_config.yml
To use retry middleware with Faraday v2.0+, install `faraday-retry` gem
            Source: /Users/hunter/dev/onboarding
       Destination: /Users/hunter/dev/onboarding/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
                    done in 1.13 seconds.
 Auto-regeneration: enabled for '/Users/hunter/dev/onboarding'
LiveReload address: http://127.0.0.1:35729
    Server address: http://127.0.0.1:4000/onboarding/
  Server running... press ctrl-c to stop.
```

Open the server address link in your browser. Every time you make changes to the project, the website will update with your changes.
