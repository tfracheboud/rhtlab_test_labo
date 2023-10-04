# Update Your Python Environment and its Libraries

We regularly update the notebooks to fix issues and add support for new libraries. 
So make sure you update this project regularly.

For this, open a terminal, and run:

    cd $HOME # or whatever development directory you chose earlier
    cd rht # go to this project's directory
    git pull

If you get an error, it's probably because you modified a notebook. 
In this case, before running `git pull` you will first need to commit your changes. 
We recommend doing this in your own branch, or else you may get conflicts:

    git checkout -b my_branch # you can use another branch name if you want
    git add -u
    git commit -m "describe your changes here"
    git checkout main
    git pull

Next, let's update the libraries. First, let's update `mamba` itself:

    mamba update -c defaults -n base conda

Then we'll delete this project's `rhtlab` environment:

    mamba activate base
    mamba env remove -n rhtlab

And recreate the environment:

    mamba env create -f environment.yml

Lastly, we reactivate the environment and start Jupyter:

    mamba activate base
    alias jlnb="jupyter lab --no-browser"
    jlnb

Then select and copy and paste into a web browser the link starting with: `http://localhost:8888/lab?token=...`.