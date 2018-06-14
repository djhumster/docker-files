The Jupyter Notebook - open-source web application
===
[The Jupyter Notebook][1] is an open-source web application that allows you to create and share documents that contain live code, equations, visualizations and narrative text. Uses include: data cleaning and transformation, numerical simulation, statistical modeling, data visualization, machine learning, and much more.

[1]:https://jupyter.org

## how-to
```
# run, after start you will get token to login http://127.0.0.1:8888
docker run --rm -p 8888:8888 --name jnotebook djhumster/jupyter-notebook

# stop
docker stop jnotebook
```