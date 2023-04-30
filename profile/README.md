## Hi there 👋

<!--

**Here are some ideas to get you started:**

🙋‍♀️ A short introduction - what is your organization all about?
🌈 Contribution guidelines - how can the community get involved?
👩‍💻 Useful resources - where can the community find your docs? Is there anything else the community should know?
🍿 Fun facts - what does your team eat for breakfast?
🧙 Remember, you can do mighty things with the power of [Markdown](https://docs.github.com/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
-->

#This is an example webapp.io configuration for Angular
FROM vm/ubuntu:18.04

# To note: Layerfiles create entire VMs, *not* containers!

# install node 10
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash && \
    apt-get install --no-install-recommends gcc g   make nodejs && \
    rm -f /etc/apt/sources.list.d/nodesource.list

# install angular CLI
RUN npm install -g @angular/cli

COPY . .
RUN npm install
RUN ng build --optimization=false
# small hack - node doesn't persist in destination of a COPY
RUN BACKGROUND ng serve --host 0.0.0.0 --disable-host-check
EXPOSE WEBSITE http://localhost:4200
