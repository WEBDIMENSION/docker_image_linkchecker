FROM python:3.9-slim


# Dependencies change on their own schedule so install them separately
RUN pip install --no-cache-dir \
    beautifulsoup4 dnspython pyxdg requests cchardet polib

RUN set -x \
    && apt-get update -qq \
    && apt-get install -y -qq --no-install-recommends git \
    && pip install --no-cache-dir git+https://github.com/linkchecker/linkchecker.git \
    && apt-get -y -qq purge git \
    && apt-get autoremove -y -qq \
    && apt-get clean -y -qq all \
    && rm -rf /var/lib/apt/lists/*

ENTRYPOINT ["linkchecker"]
