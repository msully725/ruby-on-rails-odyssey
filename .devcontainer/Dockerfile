# Use an official Ruby image as a base
FROM ruby:3.2

# Install dependencies
RUN apt-get update -qq && apt-get install -y build-essential libpq-dev nodejs sudo

# Ensure the sudoers.d directory exists, then create the vscode user
RUN mkdir -p /etc/sudoers.d \
    && useradd -m -s /bin/bash vscode \
    && echo "vscode ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/nopasswd \
    && chmod 0440 /etc/sudoers.d/nopasswd

# Set up a custom PS1 prompt with colors in .bashrc for the vscode user
RUN echo 'export PS1="\[\e[32m\]vscode\[\e[0m\]:\[\e[34m\]\w\[\e[0m\]\$ "' >> /home/vscode/.bashrc

# Set the vscode user as default (optional, can also set via devcontainer.json)
USER vscode

# Set the working directory inside the container
WORKDIR /build

# Install Bundler for dependency management
RUN gem install bundler

# Copy Gemfile and install dependencies (if you have a Gemfile)
COPY Gemfile /build/
RUN bundle install

# Expose port 3000 for Rails server
EXPOSE 3000