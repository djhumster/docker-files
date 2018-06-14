#
# Dockerfile for jupyter notebook
#
FROM python:3.6-slim-stretch

ENV JUPYTER_PORT=8888

RUN python3 -m pip install --upgrade pip \
    && python3 -m pip install jupyter

CMD jupyter notebook --port=${JUPYTER_PORT} --no-browser --ip=0.0.0.0 --allow-root