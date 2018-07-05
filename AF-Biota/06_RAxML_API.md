
## Cookbook: *RAxML* analyses in a notebook

As part of the `ipyrad.analysis` toolkit we've created convenience functions for easily running common *RAxML* commands. This can be useful when you want to run all of your analyes in a clean stream-lined way in a jupyter-notebook to create a completely reproducible study. 

### Install software
There are many ways to install raxml, the simplest of which is to use conda. This will install several raxml binaries into your conda path. If you want to call a different version of *raxml* that can easily be done by changing the parameter 'binary'. 


```python
## conda install ipyrad -c ipyrad
## conda install toytree -c eaton-lab
## conda install raxml -c bioconda
```

### Create a raxml Class object
Create a raxml object which has a bunch of default parameters associated with it. The only required argument to initialize the object is a phylip formatted sequence file. In this example I provide a name and working directory as well. 


```python
import ipyrad.analysis as ipa
import toyplot
import toytree
```


```python
rax = ipa.raxml(
    data="./analysis-ipyrad/aligntest_outfiles/aligntest.phy",
    name="aligntest", 
    workdir="analysis-raxml",
    );
```

### Additional options
You can also modify many of the other command line arguments to raxml by changing values in the params dictionary of your raxml object. These values could also have been set when you initialized the object. 


```python
## set some other params
rax.params.N = 10
rax.params.T = 2
rax.params.o = None 
#rax.params.o = ["32082_przewalskii", "33588_przewalskii"]
```

### Print the command string 
It is good practice to always print the command string so that you know exactly what was called for you analysis and it is documented. 


```python
print rax.command
```

    raxmlHPC-PTHREADS-SSE3 -f a -T 2 -m GTRGAMMA -N 10 -x 12345 -p 54321 -n aligntest -w /home/deren/Documents/ipyrad/tests/analysis-raxml -s /home/deren/Documents/ipyrad/tests/analysis-ipyrad/aligntest_outfiles/aligntest.phy


### Run the job
This will start the job running. We haven't made a progress bar yet but we will add one soon. 


```python
rax.run(force=True)
```

    job aligntest finished successfully


### Access results
One of the reasons it is so convenient to run your raxml jobs this way is that the results files are easily accessible from your raxml objects. 


```python
rax.trees
```




    bestTree                   ~/Documents/ipyrad/tests/analysis-raxml/RAxML_bestTree.aligntest
    bipartitions               ~/Documents/ipyrad/tests/analysis-raxml/RAxML_bipartitions.aligntest
    bipartitionsBranchLabels   ~/Documents/ipyrad/tests/analysis-raxml/RAxML_bipartitionsBranchLabels.aligntest
    bootstrap                  ~/Documents/ipyrad/tests/analysis-raxml/RAxML_bootstrap.aligntest
    info                       ~/Documents/ipyrad/tests/analysis-raxml/RAxML_info.aligntest



### Plot the results
Here we use toytree to plot the bootstrap results. 



```python
tre = toytree.tree(rax.trees.bipartitions)
tre.root(wildcard="3")
tre.draw(
    height=300,
    width=300,
    node_labels=tre.get_node_values("support"),
);
```


<div class="toyplot" id="tfc3e2b775c84474c888134b42658db07" style="text-align:center"><svg class="toyplot-canvas-Canvas" height="300.0px" id="t75edb7c43a7745eb8ad2d241b3edd70b" preserveAspectRatio="xMidYMid meet" style="background-color:transparent;fill:rgb(16.1%,15.3%,14.1%);fill-opacity:1.0;font-family:Helvetica;font-size:12px;opacity:1.0;stroke:rgb(16.1%,15.3%,14.1%);stroke-opacity:1.0;stroke-width:1.0" viewBox="0 0 300.0 300.0" width="300.0px" xmlns="http://www.w3.org/2000/svg" xmlns:toyplot="http://www.sandia.gov/toyplot" xmlns:xlink="http://www.w3.org/1999/xlink"><g class="toyplot-coordinates-Cartesian" id="tc4b2c837584345968c1f5a72da4fe5a5"><clipPath id="t622f113f38fc44e988fb957ac752a8be"><rect height="300.0" width="300.0" x="0.0" y="0.0"></rect></clipPath><g clip-path="url(#t622f113f38fc44e988fb957ac752a8be)"><g class="toyplot-mark-Text" id="t4fdd56f7cde84ae6bd3ad0084e033ef0"><g class="toyplot-Series"><g class="toyplot-Datum" transform="translate(224.40440894345812,56.716417910447767)"><text style="fill:rgb(16.1%,15.3%,14.1%);fill-opacity:1.0;font-family:helvetica;font-size:12.0;font-weight:normal;opacity:1.0;stroke:none;vertical-align:baseline;white-space:pre" x="15.0" y="3.066">3L_0</text></g><g class="toyplot-Datum" transform="translate(224.40440894345812,73.677069199457264)"><text style="fill:rgb(16.1%,15.3%,14.1%);fill-opacity:1.0;font-family:helvetica;font-size:12.0;font-weight:normal;opacity:1.0;stroke:none;vertical-align:baseline;white-space:pre" x="15.0" y="3.066">3K_0</text></g><g class="toyplot-Datum" transform="translate(224.40440894345812,90.637720488466769)"><text style="fill:rgb(16.1%,15.3%,14.1%);fill-opacity:1.0;font-family:helvetica;font-size:12.0;font-weight:normal;opacity:1.0;stroke:none;vertical-align:baseline;white-space:pre" x="15.0" y="3.066">3I_0</text></g><g class="toyplot-Datum" transform="translate(224.40440894345812,107.59837177747627)"><text style="fill:rgb(16.1%,15.3%,14.1%);fill-opacity:1.0;font-family:helvetica;font-size:12.0;font-weight:normal;opacity:1.0;stroke:none;vertical-align:baseline;white-space:pre" x="15.0" y="3.066">3J_0</text></g><g class="toyplot-Datum" transform="translate(224.40440894345812,124.55902306648576)"><text style="fill:rgb(16.1%,15.3%,14.1%);fill-opacity:1.0;font-family:helvetica;font-size:12.0;font-weight:normal;opacity:1.0;stroke:none;vertical-align:baseline;white-space:pre" x="15.0" y="3.066">2H_0</text></g><g class="toyplot-Datum" transform="translate(224.40440894345812,141.51967435549525)"><text style="fill:rgb(16.1%,15.3%,14.1%);fill-opacity:1.0;font-family:helvetica;font-size:12.0;font-weight:normal;opacity:1.0;stroke:none;vertical-align:baseline;white-space:pre" x="15.0" y="3.066">2G_0</text></g><g class="toyplot-Datum" transform="translate(224.40440894345812,158.48032564450475)"><text style="fill:rgb(16.1%,15.3%,14.1%);fill-opacity:1.0;font-family:helvetica;font-size:12.0;font-weight:normal;opacity:1.0;stroke:none;vertical-align:baseline;white-space:pre" x="15.0" y="3.066">2F_0</text></g><g class="toyplot-Datum" transform="translate(224.40440894345812,175.44097693351426)"><text style="fill:rgb(16.1%,15.3%,14.1%);fill-opacity:1.0;font-family:helvetica;font-size:12.0;font-weight:normal;opacity:1.0;stroke:none;vertical-align:baseline;white-space:pre" x="15.0" y="3.066">2E_0</text></g><g class="toyplot-Datum" transform="translate(224.40440894345812,192.40162822252375)"><text style="fill:rgb(16.1%,15.3%,14.1%);fill-opacity:1.0;font-family:helvetica;font-size:12.0;font-weight:normal;opacity:1.0;stroke:none;vertical-align:baseline;white-space:pre" x="15.0" y="3.066">1D_0</text></g><g class="toyplot-Datum" transform="translate(224.40440894345812,209.36227951153325)"><text style="fill:rgb(16.1%,15.3%,14.1%);fill-opacity:1.0;font-family:helvetica;font-size:12.0;font-weight:normal;opacity:1.0;stroke:none;vertical-align:baseline;white-space:pre" x="15.0" y="3.066">1C_0</text></g><g class="toyplot-Datum" transform="translate(224.40440894345812,226.32293080054276)"><text style="fill:rgb(16.1%,15.3%,14.1%);fill-opacity:1.0;font-family:helvetica;font-size:12.0;font-weight:normal;opacity:1.0;stroke:none;vertical-align:baseline;white-space:pre" x="15.0" y="3.066">1B_0</text></g><g class="toyplot-Datum" transform="translate(224.40440894345812,243.28358208955225)"><text style="fill:rgb(16.1%,15.3%,14.1%);fill-opacity:1.0;font-family:helvetica;font-size:12.0;font-weight:normal;opacity:1.0;stroke:none;vertical-align:baseline;white-space:pre" x="15.0" y="3.066">1A_0</text></g></g></g><g class="toyplot-mark-Graph" id="t4ae090c4243749889d4be33e905785f0"><g class="toyplot-Edges"><path d="M 50.0 122.438941655 L 50.0 71.5569877883" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 50.0 71.5569877883 L 119.761763577 71.5569877883" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 50.0 122.438941655 L 50.0 173.320895522" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 50.0 173.320895522 L 84.8808817887 173.320895522" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 119.761763577 71.5569877883 L 119.761763577 56.7164179104" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 119.761763577 56.7164179104 L 224.404408943 56.7164179104" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 119.761763577 71.5569877883 L 119.761763577 86.3975576662" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 119.761763577 86.3975576662 L 154.642645366 86.3975576662" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 84.8808817887 173.320895522 L 84.8808817887 139.399592944" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 84.8808817887 139.399592944 L 119.761763577 139.399592944" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 84.8808817887 173.320895522 L 84.8808817887 207.2421981" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 84.8808817887 207.2421981 L 119.761763577 207.2421981" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.642645366 86.3975576662 L 154.642645366 73.6770691995" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.642645366 73.6770691995 L 224.404408943 73.6770691995" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.642645366 86.3975576662 L 154.642645366 99.118046133" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.642645366 99.118046133 L 189.523527155 99.118046133" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 119.761763577 139.399592944 L 119.761763577 124.559023066" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 119.761763577 124.559023066 L 224.404408943 124.559023066" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 119.761763577 139.399592944 L 119.761763577 154.240162822" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 119.761763577 154.240162822 L 154.642645366 154.240162822" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 119.761763577 207.2421981 L 119.761763577 192.401628223" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 119.761763577 192.401628223 L 224.404408943 192.401628223" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 119.761763577 207.2421981 L 119.761763577 222.082767978" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 119.761763577 222.082767978 L 154.642645366 222.082767978" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 189.523527155 99.118046133 L 189.523527155 90.6377204885" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 189.523527155 90.6377204885 L 224.404408943 90.6377204885" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 189.523527155 99.118046133 L 189.523527155 107.598371777" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 189.523527155 107.598371777 L 224.404408943 107.598371777" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.642645366 154.240162822 L 154.642645366 141.519674355" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.642645366 141.519674355 L 224.404408943 141.519674355" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.642645366 154.240162822 L 154.642645366 166.960651289" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.642645366 166.960651289 L 189.523527155 166.960651289" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.642645366 222.082767978 L 154.642645366 209.362279512" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.642645366 209.362279512 L 224.404408943 209.362279512" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.642645366 222.082767978 L 154.642645366 234.803256445" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.642645366 234.803256445 L 189.523527155 234.803256445" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 189.523527155 166.960651289 L 189.523527155 158.480325645" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 189.523527155 158.480325645 L 224.404408943 158.480325645" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 189.523527155 166.960651289 L 189.523527155 175.440976934" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 189.523527155 175.440976934 L 224.404408943 175.440976934" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 189.523527155 234.803256445 L 189.523527155 226.322930801" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 189.523527155 226.322930801 L 224.404408943 226.322930801" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 189.523527155 234.803256445 L 189.523527155 243.28358209" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 189.523527155 243.28358209 L 224.404408943 243.28358209" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path></g><g class="toyplot-Vertices"><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="50.0" cy="122.43894165535957" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="50.0" cy="71.556987788331085" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="119.76176357738325" cy="71.556987788331085" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="50.0" cy="173.32089552238807" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="84.880881788691624" cy="173.32089552238807" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="119.76176357738325" cy="71.556987788331085" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="119.76176357738325" cy="56.716417910447767" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="224.40440894345812" cy="56.716417910447767" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="119.76176357738325" cy="86.397557666214396" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.64264536607487" cy="86.397557666214396" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="84.880881788691624" cy="173.32089552238807" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="84.880881788691624" cy="139.39959294436909" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="119.76176357738325" cy="139.39959294436909" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="84.880881788691624" cy="207.24219810040705" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="119.76176357738325" cy="207.24219810040705" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.64264536607487" cy="86.397557666214396" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.64264536607487" cy="73.677069199457264" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="224.40440894345812" cy="73.677069199457264" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.64264536607487" cy="99.118046132971529" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="189.5235271547665" cy="99.118046132971529" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="119.76176357738325" cy="139.39959294436909" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="119.76176357738325" cy="124.55902306648576" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="224.40440894345812" cy="124.55902306648576" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="119.76176357738325" cy="154.24016282225239" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.64264536607487" cy="154.24016282225239" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="119.76176357738325" cy="207.24219810040705" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="119.76176357738325" cy="192.40162822252375" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="224.40440894345812" cy="192.40162822252375" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="119.76176357738325" cy="222.08276797829038" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.64264536607487" cy="222.08276797829038" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="189.5235271547665" cy="99.118046132971529" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="189.5235271547665" cy="90.637720488466769" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="224.40440894345812" cy="90.637720488466769" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="189.5235271547665" cy="107.59837177747627" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="224.40440894345812" cy="107.59837177747627" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.64264536607487" cy="154.24016282225239" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.64264536607487" cy="141.51967435549525" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="224.40440894345812" cy="141.51967435549525" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.64264536607487" cy="166.96065128900952" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="189.5235271547665" cy="166.96065128900952" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.64264536607487" cy="222.08276797829038" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.64264536607487" cy="209.36227951153325" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="224.40440894345812" cy="209.36227951153325" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.64264536607487" cy="234.80325644504748" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="189.5235271547665" cy="234.80325644504748" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="189.5235271547665" cy="166.96065128900952" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="189.5235271547665" cy="158.48032564450475" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="224.40440894345812" cy="158.48032564450475" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="189.5235271547665" cy="175.44097693351426" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="224.40440894345812" cy="175.44097693351426" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="189.5235271547665" cy="234.80325644504748" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="189.5235271547665" cy="226.32293080054276" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="224.40440894345812" cy="226.32293080054276" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="189.5235271547665" cy="243.28358208955225" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="224.40440894345812" cy="243.28358208955225" r="0.0"></circle></g></g></g><g class="toyplot-mark-Scatterplot" id="t61e8106d864c488796273f9d25ec1413"><g class="toyplot-Series"><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:none"><title>idx: 1
name: 7
dist: 0.00306813286161
support: 100</title><circle cx="119.76176357738325" cy="71.556987788331085" r="11.0"></circle><g transform="translate(119.76176357738325,71.556987788331085)"><text style="fill:rgb(14.9%,14.9%,14.9%);fill-opacity:1.0;font-family:helvetica;font-size:9.0;font-weight:normal;stroke:none;vertical-align:baseline;white-space:pre" x="-10.506" y="3.7995">100</text></g></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:none"><title>idx: 2
name: 8
dist: 0.000958273347783
support: 100</title><circle cx="154.64264536607487" cy="86.397557666214396" r="11.0"></circle><g transform="translate(154.64264536607487,86.397557666214396)"><text style="fill:rgb(14.9%,14.9%,14.9%);fill-opacity:1.0;font-family:helvetica;font-size:9.0;font-weight:normal;stroke:none;vertical-align:baseline;white-space:pre" x="-10.506" y="3.7995">100</text></g></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:none"><title>idx: 3
name: 9
dist: 0.00106650019095
support: 100</title><circle cx="189.5235271547665" cy="99.118046132971529" r="11.0"></circle><g transform="translate(189.5235271547665,99.118046132971529)"><text style="fill:rgb(14.9%,14.9%,14.9%);fill-opacity:1.0;font-family:helvetica;font-size:9.0;font-weight:normal;stroke:none;vertical-align:baseline;white-space:pre" x="-10.506" y="3.7995">100</text></g></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:none"><title>idx: 4
name: 3
dist: 0.00306813286161
support: 100</title><circle cx="84.880881788691624" cy="173.32089552238807" r="11.0"></circle><g transform="translate(84.880881788691624,173.32089552238807)"><text style="fill:rgb(14.9%,14.9%,14.9%);fill-opacity:1.0;font-family:helvetica;font-size:9.0;font-weight:normal;stroke:none;vertical-align:baseline;white-space:pre" x="-10.506" y="3.7995">100</text></g></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:none"><title>idx: 5
name: 4
dist: 0.000973067754965
support: 100</title><circle cx="119.76176357738325" cy="139.39959294436909" r="11.0"></circle><g transform="translate(119.76176357738325,139.39959294436909)"><text style="fill:rgb(14.9%,14.9%,14.9%);fill-opacity:1.0;font-family:helvetica;font-size:9.0;font-weight:normal;stroke:none;vertical-align:baseline;white-space:pre" x="-10.506" y="3.7995">100</text></g></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:none"><title>idx: 6
name: 5
dist: 0.00117656048502
support: 100</title><circle cx="154.64264536607487" cy="154.24016282225239" r="11.0"></circle><g transform="translate(154.64264536607487,154.24016282225239)"><text style="fill:rgb(14.9%,14.9%,14.9%);fill-opacity:1.0;font-family:helvetica;font-size:9.0;font-weight:normal;stroke:none;vertical-align:baseline;white-space:pre" x="-10.506" y="3.7995">100</text></g></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:none"><title>idx: 7
name: 6
dist: 0.00116405198144
support: 100</title><circle cx="189.5235271547665" cy="166.96065128900952" r="11.0"></circle><g transform="translate(189.5235271547665,166.96065128900952)"><text style="fill:rgb(14.9%,14.9%,14.9%);fill-opacity:1.0;font-family:helvetica;font-size:9.0;font-weight:normal;stroke:none;vertical-align:baseline;white-space:pre" x="-10.506" y="3.7995">100</text></g></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:none"><title>idx: 8
name: 2
dist: 0.00107367225634
support: 100</title><circle cx="119.76176357738325" cy="207.24219810040705" r="11.0"></circle><g transform="translate(119.76176357738325,207.24219810040705)"><text style="fill:rgb(14.9%,14.9%,14.9%);fill-opacity:1.0;font-family:helvetica;font-size:9.0;font-weight:normal;stroke:none;vertical-align:baseline;white-space:pre" x="-10.506" y="3.7995">100</text></g></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:none"><title>idx: 9
name: 1
dist: 0.00105363755445
support: 100</title><circle cx="154.64264536607487" cy="222.08276797829038" r="11.0"></circle><g transform="translate(154.64264536607487,222.08276797829038)"><text style="fill:rgb(14.9%,14.9%,14.9%);fill-opacity:1.0;font-family:helvetica;font-size:9.0;font-weight:normal;stroke:none;vertical-align:baseline;white-space:pre" x="-10.506" y="3.7995">100</text></g></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:none"><title>idx: 10
name: 10
dist: 0.00110599233987
support: 100</title><circle cx="189.5235271547665" cy="234.80325644504748" r="11.0"></circle><g transform="translate(189.5235271547665,234.80325644504748)"><text style="fill:rgb(14.9%,14.9%,14.9%);fill-opacity:1.0;font-family:helvetica;font-size:9.0;font-weight:normal;stroke:none;vertical-align:baseline;white-space:pre" x="-10.506" y="3.7995">100</text></g></g></g></g></g></g></svg><div class="toyplot-behavior"><script>(function()
{
var modules={};
modules["toyplot/tables"] = (function()
    {
        var tables = [];

        var module = {};

        module.store = function(owner, key, names, columns)
        {
            tables.push({owner: owner, key: key, names: names, columns: columns});
        }

        module.get_csv = function(owner, key)
        {
            var csv = "";
            for(var i = 0; i != tables.length; ++i)
            {
                var table = tables[i];
                if(table.owner != owner)
                    continue;
                if(table.key != key)
                    continue;

                csv += table.names.join(",") + "\n";
                for(var i = 0; i != table.columns[0].length; ++i)
                {
                  for(var j = 0; j != table.columns.length; ++j)
                  {
                    if(j)
                      csv += ",";
                    csv += table.columns[j][i];
                  }
                  csv += "\n";
                }
                return csv;
            }
        }

        return module;
    })();
modules["toyplot/root/id"] = "tfc3e2b775c84474c888134b42658db07";
modules["toyplot/root"] = (function(root_id)
    {
        return document.querySelector("#" + root_id);
    })(modules["toyplot/root/id"]);
modules["toyplot/canvas/id"] = "t75edb7c43a7745eb8ad2d241b3edd70b";
modules["toyplot/canvas"] = (function(canvas_id)
    {
        return document.querySelector("#" + canvas_id);
    })(modules["toyplot/canvas/id"]);
modules["toyplot/menus/context"] = (function(root, canvas)
    {
        var wrapper = document.createElement("div");
        wrapper.innerHTML = "<ul class='toyplot-context-menu' style='background:#eee; border:1px solid #b8b8b8; border-radius:5px; box-shadow: 0px 0px 8px rgba(0%,0%,0%,0.25); margin:0; padding:3px 0; position:fixed; visibility:hidden;'></ul>"
        var menu = wrapper.firstChild;

        root.appendChild(menu);

        var items = [];

        var ignore_mouseup = null;
        function open_menu(e)
        {
            var show_menu = false;
            for(var index=0; index != items.length; ++index)
            {
                var item = items[index];
                if(item.show(e))
                {
                    item.item.style.display = "block";
                    show_menu = true;
                }
                else
                {
                    item.item.style.display = "none";
                }
            }

            if(show_menu)
            {
                ignore_mouseup = true;
                menu.style.left = (e.clientX + 1) + "px";
                menu.style.top = (e.clientY - 5) + "px";
                menu.style.visibility = "visible";
                e.stopPropagation();
                e.preventDefault();
            }
        }

        function close_menu()
        {
            menu.style.visibility = "hidden";
        }

        function contextmenu(e)
        {
            open_menu(e);
        }

        function mousemove(e)
        {
            ignore_mouseup = false;
        }

        function mouseup(e)
        {
            if(ignore_mouseup)
            {
                ignore_mouseup = false;
                return;
            }
            close_menu();
        }

        function keydown(e)
        {
            if(e.key == "Escape" || e.key == "Esc" || e.keyCode == 27)
            {
                close_menu();
            }
        }

        canvas.addEventListener("contextmenu", contextmenu);
        canvas.addEventListener("mousemove", mousemove);
        document.addEventListener("mouseup", mouseup);
        document.addEventListener("keydown", keydown);

        var module = {};
        module.add_item = function(label, show_callback, choose_callback)
        {
            var wrapper = document.createElement("div");
            wrapper.innerHTML = "<li class='toyplot-context-menu-item' style='background:#eee; color:#333; padding:2px 20px; list-style:none; margin:0; text-align:left;'>" + label + "</li>"
            var item = wrapper.firstChild;

            items.push({item: item, show: show_callback});

            function mouseover()
            {
                this.style.background = "steelblue";
                this.style.color = "white";
            }

            function mouseout()
            {
                this.style.background = "#eee";
                this.style.color = "#333";
            }

            function choose_item(e)
            {
                close_menu();
                choose_callback();

                e.stopPropagation();
                e.preventDefault();
            }

            item.addEventListener("mouseover", mouseover);
            item.addEventListener("mouseout", mouseout);
            item.addEventListener("mouseup", choose_item);
            item.addEventListener("contextmenu", choose_item);

            menu.appendChild(item);
        };
        return module;
    })(modules["toyplot/root"],modules["toyplot/canvas"]);
modules["toyplot/io"] = (function()
    {
        var module = {};
        module.save_file = function(mime_type, charset, data, filename)
        {
            var uri = "data:" + mime_type + ";charset=" + charset + "," + data;
            uri = encodeURI(uri);

            var link = document.createElement("a");
            if(typeof link.download != "undefined")
            {
              link.href = uri;
              link.style = "visibility:hidden";
              link.download = filename;

              document.body.appendChild(link);
              link.click();
              document.body.removeChild(link);
            }
            else
            {
              window.open(uri);
            }
        };
        return module;
    })();
(function(tables, context_menu, io, owner_id, key, label, names, columns, filename)
        {
            tables.store(owner_id, key, names, columns);

            var owner = document.querySelector("#" + owner_id);
            function show_item(e)
            {
                return owner.contains(e.target);
            }

            function choose_item()
            {
                io.save_file("text/csv", "utf-8", tables.get_csv(owner_id, key), filename + ".csv");
            }

            context_menu.add_item("Save " + label + " as CSV", show_item, choose_item);
        })(modules["toyplot/tables"],modules["toyplot/menus/context"],modules["toyplot/io"],"t4ae090c4243749889d4be33e905785f0","vertex_data","graph vertex data",["x", "y"],[[-5.0, -5.0, -3.0, -5.0, -4.0, -3.0, -3.0, 0.0, -3.0, -2.0, -4.0, -4.0, -3.0, -4.0, -3.0, -2.0, -2.0, 0.0, -2.0, -1.0, -3.0, -3.0, 0.0, -3.0, -2.0, -3.0, -3.0, 0.0, -3.0, -2.0, -1.0, -1.0, 0.0, -1.0, 0.0, -2.0, -2.0, 0.0, -2.0, -1.0, -2.0, -2.0, 0.0, -2.0, -1.0, -1.0, -1.0, 0.0, -1.0, 0.0, -1.0, -1.0, 0.0, -1.0, 0.0], [7.125, 10.125, 10.125, 4.125, 4.125, 10.125, 11.0, 11.0, 9.25, 9.25, 4.125, 6.125, 6.125, 2.125, 2.125, 9.25, 10.0, 10.0, 8.5, 8.5, 6.125, 7.0, 7.0, 5.25, 5.25, 2.125, 3.0, 3.0, 1.25, 1.25, 8.5, 9.0, 9.0, 8.0, 8.0, 5.25, 6.0, 6.0, 4.5, 4.5, 1.25, 2.0, 2.0, 0.5, 0.5, 4.5, 5.0, 5.0, 4.0, 4.0, 0.5, 1.0, 1.0, 0.0, 0.0]],"toyplot");
(function(tables, context_menu, io, owner_id, key, label, names, columns, filename)
        {
            tables.store(owner_id, key, names, columns);

            var owner = document.querySelector("#" + owner_id);
            function show_item(e)
            {
                return owner.contains(e.target);
            }

            function choose_item()
            {
                io.save_file("text/csv", "utf-8", tables.get_csv(owner_id, key), filename + ".csv");
            }

            context_menu.add_item("Save " + label + " as CSV", show_item, choose_item);
        })(modules["toyplot/tables"],modules["toyplot/menus/context"],modules["toyplot/io"],"t4ae090c4243749889d4be33e905785f0","edge_data","graph edge data",["source", "target"],[[0, 1, 0, 3, 5, 6, 5, 8, 10, 11, 10, 13, 15, 16, 15, 18, 20, 21, 20, 23, 25, 26, 25, 28, 30, 31, 30, 33, 35, 36, 35, 38, 40, 41, 40, 43, 45, 46, 45, 48, 50, 51, 50, 53], [1, 2, 3, 4, 6, 7, 8, 9, 11, 12, 13, 14, 16, 17, 18, 19, 21, 22, 23, 24, 26, 27, 28, 29, 31, 32, 33, 34, 36, 37, 38, 39, 41, 42, 43, 44, 46, 47, 48, 49, 51, 52, 53, 54]],"toyplot");
(function(tables, context_menu, io, owner_id, key, label, names, columns, filename)
        {
            tables.store(owner_id, key, names, columns);

            var owner = document.querySelector("#" + owner_id);
            function show_item(e)
            {
                return owner.contains(e.target);
            }

            function choose_item()
            {
                io.save_file("text/csv", "utf-8", tables.get_csv(owner_id, key), filename + ".csv");
            }

            context_menu.add_item("Save " + label + " as CSV", show_item, choose_item);
        })(modules["toyplot/tables"],modules["toyplot/menus/context"],modules["toyplot/io"],"t61e8106d864c488796273f9d25ec1413","data","scatterplot",["x", "y0"],[[-5.0, -3.0, -2.0, -1.0, -4.0, -3.0, -2.0, -1.0, -3.0, -2.0, -1.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0], [7.125, 10.125, 9.25, 8.5, 4.125, 6.125, 5.25, 4.5, 2.125, 1.25, 0.5, 11.0, 10.0, 9.0, 8.0, 7.0, 6.0, 5.0, 4.0, 3.0, 2.0, 1.0, 0.0]],"toyplot");
})();</script></div></div>


## [optional] Submit raxml jobs to run on a cluster
Using the ipyparallel library you can submit raxml jobs to run in parallel on cluster in a load-balanced fashion. You can then tell the notebook to wait until all jobs are finished before progressing in the notebook to draw trees, etc. 

#### Start an ipyparallel cluster
In a separate terminal start an `ipcluster` instance and tell it how many engines to start. 


```python
##
##  ipcluster start --n=20
##
```

Create a Client connected to the cluster


```python
import ipyparallel as ipp
ipyclient = ipp.Client()
```

Create several raxml objects for different data sets


```python
rax1 = ipa.raxml(
    data="~/Documents/ipyrad/tests/analysis-ipyrad/pedic_outfiles/pedic.phy", 
    name="rax1", T=4, N=100)

rax2 = ipa.raxml(
    data="~/Documents/ipyrad/tests/analysis-ipyrad/aligntest_outfiles/aligntest.phy", 
    name="rax2", T=4, N=100)
```

Submit jobs to run on the cluster queue. 


```python
rax1.run(ipyclient=ipyclient, force=True)
rax2.run(ipyclient=ipyclient, force=True)
```

    job rax1 submitted to cluster
    job rax2 submitted to cluster


Wait for jobs to finish


```python
## you can query each job while it's running
rax1.async.ready()
```




    True




```python
## or just block until all jobs on ipyclient are finished
ipyclient.wait()
```




    True



### Plot trees when jobs are finished
Here we will draw a slighly more complex tree figure that combines two trees onto a single canvas.


```python
## load trees and add to axes
tre1 = toytree.tree(rax1.trees.bipartitions)
tre1.root(wildcard="prz")
tre1.draw(width=300);

tre2 = toytree.tree(rax2.trees.bipartitions)
tre2.root(wildcard="3")
tre2.draw(width=300);
```


<div class="toyplot" id="t8e5d0d5640f442f78e890290e8d24852" style="text-align:center"><svg class="toyplot-canvas-Canvas" height="300.0px" id="t437be2283ac8475cba05e25d61d84949" preserveAspectRatio="xMidYMid meet" style="background-color:transparent;fill:rgb(16.1%,15.3%,14.1%);fill-opacity:1.0;font-family:Helvetica;font-size:12px;opacity:1.0;stroke:rgb(16.1%,15.3%,14.1%);stroke-opacity:1.0;stroke-width:1.0" viewBox="0 0 300.0 300.0" width="300.0px" xmlns="http://www.w3.org/2000/svg" xmlns:toyplot="http://www.sandia.gov/toyplot" xmlns:xlink="http://www.w3.org/1999/xlink"><g class="toyplot-coordinates-Cartesian" id="t7ceaf757ae8c433d81de283631f2404b"><clipPath id="t98fe35dc81fa4fc9a1291a82c3d6a67e"><rect height="300.0" width="300.0" x="0.0" y="0.0"></rect></clipPath><g clip-path="url(#t98fe35dc81fa4fc9a1291a82c3d6a67e)"><g class="toyplot-mark-Text" id="t8490270e0b0b40eeb6bb80cf649816dd"><g class="toyplot-Series"><g class="toyplot-Datum" transform="translate(171.6781855348973,56.716417910447767)"><text style="fill:rgb(16.1%,15.3%,14.1%);fill-opacity:1.0;font-family:helvetica;font-size:12.0;font-weight:normal;opacity:1.0;stroke:none;vertical-align:baseline;white-space:pre" x="15.0" y="3.066">32082_przewalskii</text></g><g class="toyplot-Datum" transform="translate(171.6781855348973,72.263681592039816)"><text style="fill:rgb(16.1%,15.3%,14.1%);fill-opacity:1.0;font-family:helvetica;font-size:12.0;font-weight:normal;opacity:1.0;stroke:none;vertical-align:baseline;white-space:pre" x="15.0" y="3.066">33588_przewalskii</text></g><g class="toyplot-Datum" transform="translate(171.6781855348973,87.810945273631845)"><text style="fill:rgb(16.1%,15.3%,14.1%);fill-opacity:1.0;font-family:helvetica;font-size:12.0;font-weight:normal;opacity:1.0;stroke:none;vertical-align:baseline;white-space:pre" x="15.0" y="3.066">29154_superba</text></g><g class="toyplot-Datum" transform="translate(171.6781855348973,103.35820895522389)"><text style="fill:rgb(16.1%,15.3%,14.1%);fill-opacity:1.0;font-family:helvetica;font-size:12.0;font-weight:normal;opacity:1.0;stroke:none;vertical-align:baseline;white-space:pre" x="15.0" y="3.066">30686_cyathophylla</text></g><g class="toyplot-Datum" transform="translate(171.6781855348973,118.90547263681592)"><text style="fill:rgb(16.1%,15.3%,14.1%);fill-opacity:1.0;font-family:helvetica;font-size:12.0;font-weight:normal;opacity:1.0;stroke:none;vertical-align:baseline;white-space:pre" x="15.0" y="3.066">41478_cyathophylloides</text></g><g class="toyplot-Datum" transform="translate(171.6781855348973,134.45273631840794)"><text style="fill:rgb(16.1%,15.3%,14.1%);fill-opacity:1.0;font-family:helvetica;font-size:12.0;font-weight:normal;opacity:1.0;stroke:none;vertical-align:baseline;white-space:pre" x="15.0" y="3.066">41954_cyathophylloides</text></g><g class="toyplot-Datum" transform="translate(171.6781855348973,150.0)"><text style="fill:rgb(16.1%,15.3%,14.1%);fill-opacity:1.0;font-family:helvetica;font-size:12.0;font-weight:normal;opacity:1.0;stroke:none;vertical-align:baseline;white-space:pre" x="15.0" y="3.066">33413_thamno</text></g><g class="toyplot-Datum" transform="translate(171.6781855348973,165.54726368159203)"><text style="fill:rgb(16.1%,15.3%,14.1%);fill-opacity:1.0;font-family:helvetica;font-size:12.0;font-weight:normal;opacity:1.0;stroke:none;vertical-align:baseline;white-space:pre" x="15.0" y="3.066">30556_thamno</text></g><g class="toyplot-Datum" transform="translate(171.6781855348973,181.09452736318408)"><text style="fill:rgb(16.1%,15.3%,14.1%);fill-opacity:1.0;font-family:helvetica;font-size:12.0;font-weight:normal;opacity:1.0;stroke:none;vertical-align:baseline;white-space:pre" x="15.0" y="3.066">40578_rex</text></g><g class="toyplot-Datum" transform="translate(171.6781855348973,196.64179104477611)"><text style="fill:rgb(16.1%,15.3%,14.1%);fill-opacity:1.0;font-family:helvetica;font-size:12.0;font-weight:normal;opacity:1.0;stroke:none;vertical-align:baseline;white-space:pre" x="15.0" y="3.066">35855_rex</text></g><g class="toyplot-Datum" transform="translate(171.6781855348973,212.18905472636817)"><text style="fill:rgb(16.1%,15.3%,14.1%);fill-opacity:1.0;font-family:helvetica;font-size:12.0;font-weight:normal;opacity:1.0;stroke:none;vertical-align:baseline;white-space:pre" x="15.0" y="3.066">35236_rex</text></g><g class="toyplot-Datum" transform="translate(171.6781855348973,227.7363184079602)"><text style="fill:rgb(16.1%,15.3%,14.1%);fill-opacity:1.0;font-family:helvetica;font-size:12.0;font-weight:normal;opacity:1.0;stroke:none;vertical-align:baseline;white-space:pre" x="15.0" y="3.066">38362_rex</text></g><g class="toyplot-Datum" transform="translate(171.6781855348973,243.28358208955225)"><text style="fill:rgb(16.1%,15.3%,14.1%);fill-opacity:1.0;font-family:helvetica;font-size:12.0;font-weight:normal;opacity:1.0;stroke:none;vertical-align:baseline;white-space:pre" x="15.0" y="3.066">39618_rex</text></g></g></g><g class="toyplot-mark-Graph" id="t81a655794c954831b08cff7175db3762"><g class="toyplot-Edges"><path d="M 50.0 102.022115983 L 50.0 64.4900497512" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 50.0 64.4900497512 L 154.295587601 64.4900497512" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 50.0 102.022115983 L 50.0 139.554182214" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 50.0 139.554182214 L 67.3825979336 139.554182214" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.295587601 64.4900497512 L 154.295587601 56.7164179104" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.295587601 56.7164179104 L 171.678185535 56.7164179104" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.295587601 64.4900497512 L 154.295587601 72.263681592" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.295587601 72.263681592 L 171.678185535 72.263681592" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 67.3825979336 139.554182214 L 67.3825979336 111.131840796" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 67.3825979336 111.131840796 L 136.912989668 111.131840796" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 67.3825979336 139.554182214 L 67.3825979336 167.976523632" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 67.3825979336 167.976523632 L 84.7651958671 167.976523632" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 136.912989668 111.131840796 L 136.912989668 95.5845771144" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 136.912989668 95.5845771144 L 154.295587601 95.5845771144" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 136.912989668 111.131840796 L 136.912989668 126.679104478" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 136.912989668 126.679104478 L 154.295587601 126.679104478" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 84.7651958671 167.976523632 L 84.7651958671 150.0" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 84.7651958671 150.0 L 171.678185535 150.0" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 84.7651958671 167.976523632 L 84.7651958671 185.953047264" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 84.7651958671 185.953047264 L 102.147793801 185.953047264" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.295587601 95.5845771144 L 154.295587601 87.8109452736" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.295587601 87.8109452736 L 171.678185535 87.8109452736" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.295587601 95.5845771144 L 154.295587601 103.358208955" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.295587601 103.358208955 L 171.678185535 103.358208955" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.295587601 126.679104478 L 154.295587601 118.905472637" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.295587601 118.905472637 L 171.678185535 118.905472637" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.295587601 126.679104478 L 154.295587601 134.452736318" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.295587601 134.452736318 L 171.678185535 134.452736318" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 102.147793801 185.953047264 L 102.147793801 165.547263682" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 102.147793801 165.547263682 L 171.678185535 165.547263682" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 102.147793801 185.953047264 L 102.147793801 206.358830846" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 102.147793801 206.358830846 L 119.530391734 206.358830846" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 119.530391734 206.358830846 L 119.530391734 188.868159204" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 119.530391734 188.868159204 L 154.295587601 188.868159204" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 119.530391734 206.358830846 L 119.530391734 223.849502488" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 119.530391734 223.849502488 L 136.912989668 223.849502488" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.295587601 188.868159204 L 154.295587601 181.094527363" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.295587601 181.094527363 L 171.678185535 181.094527363" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.295587601 188.868159204 L 154.295587601 196.641791045" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.295587601 196.641791045 L 171.678185535 196.641791045" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 136.912989668 223.849502488 L 136.912989668 212.189054726" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 136.912989668 212.189054726 L 171.678185535 212.189054726" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 136.912989668 223.849502488 L 136.912989668 235.509950249" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 136.912989668 235.509950249 L 154.295587601 235.509950249" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.295587601 235.509950249 L 154.295587601 227.736318408" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.295587601 227.736318408 L 171.678185535 227.736318408" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.295587601 235.509950249 L 154.295587601 243.28358209" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.295587601 243.28358209 L 171.678185535 243.28358209" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path></g><g class="toyplot-Vertices"><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="50.0" cy="102.02211598258708" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="50.0" cy="64.490049751243788" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.29558760134054" cy="64.490049751243788" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="50.0" cy="139.55418221393035" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="67.382597933556752" cy="139.55418221393035" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.29558760134054" cy="64.490049751243788" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.29558760134054" cy="56.716417910447767" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="171.6781855348973" cy="56.716417910447767" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.29558760134054" cy="72.263681592039816" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="171.6781855348973" cy="72.263681592039816" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="67.382597933556752" cy="139.55418221393035" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="67.382597933556752" cy="111.13184079601993" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="136.91298966778379" cy="111.13184079601993" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="67.382597933556752" cy="167.97652363184082" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="84.765195867113505" cy="167.97652363184082" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="136.91298966778379" cy="111.13184079601993" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="136.91298966778379" cy="95.584577114427873" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.29558760134054" cy="95.584577114427873" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="136.91298966778379" cy="126.67910447761196" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.29558760134054" cy="126.67910447761196" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="84.765195867113505" cy="167.97652363184082" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="84.765195867113505" cy="150.0" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="171.6781855348973" cy="150.0" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="84.765195867113505" cy="185.95304726368158" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="102.14779380067027" cy="185.95304726368158" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.29558760134054" cy="95.584577114427873" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.29558760134054" cy="87.810945273631845" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="171.6781855348973" cy="87.810945273631845" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.29558760134054" cy="103.35820895522389" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="171.6781855348973" cy="103.35820895522389" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.29558760134054" cy="126.67910447761196" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.29558760134054" cy="118.90547263681592" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="171.6781855348973" cy="118.90547263681592" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.29558760134054" cy="134.45273631840794" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="171.6781855348973" cy="134.45273631840794" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="102.14779380067027" cy="185.95304726368158" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="102.14779380067027" cy="165.54726368159203" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="171.6781855348973" cy="165.54726368159203" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="102.14779380067027" cy="206.35883084577114" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="119.53039173422702" cy="206.35883084577114" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="119.53039173422702" cy="206.35883084577114" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="119.53039173422702" cy="188.8681592039801" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.29558760134054" cy="188.8681592039801" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="119.53039173422702" cy="223.84950248756221" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="136.91298966778379" cy="223.84950248756221" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.29558760134054" cy="188.8681592039801" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.29558760134054" cy="181.09452736318408" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="171.6781855348973" cy="181.09452736318408" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.29558760134054" cy="196.64179104477611" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="171.6781855348973" cy="196.64179104477611" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="136.91298966778379" cy="223.84950248756221" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="136.91298966778379" cy="212.18905472636817" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="171.6781855348973" cy="212.18905472636817" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="136.91298966778379" cy="235.50995024875621" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.29558760134054" cy="235.50995024875621" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.29558760134054" cy="235.50995024875621" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.29558760134054" cy="227.7363184079602" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="171.6781855348973" cy="227.7363184079602" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.29558760134054" cy="243.28358208955225" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="171.6781855348973" cy="243.28358208955225" r="0.0"></circle></g></g></g></g></g></svg><div class="toyplot-behavior"><script>(function()
{
var modules={};
modules["toyplot/tables"] = (function()
    {
        var tables = [];

        var module = {};

        module.store = function(owner, key, names, columns)
        {
            tables.push({owner: owner, key: key, names: names, columns: columns});
        }

        module.get_csv = function(owner, key)
        {
            var csv = "";
            for(var i = 0; i != tables.length; ++i)
            {
                var table = tables[i];
                if(table.owner != owner)
                    continue;
                if(table.key != key)
                    continue;

                csv += table.names.join(",") + "\n";
                for(var i = 0; i != table.columns[0].length; ++i)
                {
                  for(var j = 0; j != table.columns.length; ++j)
                  {
                    if(j)
                      csv += ",";
                    csv += table.columns[j][i];
                  }
                  csv += "\n";
                }
                return csv;
            }
        }

        return module;
    })();
modules["toyplot/root/id"] = "t8e5d0d5640f442f78e890290e8d24852";
modules["toyplot/root"] = (function(root_id)
    {
        return document.querySelector("#" + root_id);
    })(modules["toyplot/root/id"]);
modules["toyplot/canvas/id"] = "t437be2283ac8475cba05e25d61d84949";
modules["toyplot/canvas"] = (function(canvas_id)
    {
        return document.querySelector("#" + canvas_id);
    })(modules["toyplot/canvas/id"]);
modules["toyplot/menus/context"] = (function(root, canvas)
    {
        var wrapper = document.createElement("div");
        wrapper.innerHTML = "<ul class='toyplot-context-menu' style='background:#eee; border:1px solid #b8b8b8; border-radius:5px; box-shadow: 0px 0px 8px rgba(0%,0%,0%,0.25); margin:0; padding:3px 0; position:fixed; visibility:hidden;'></ul>"
        var menu = wrapper.firstChild;

        root.appendChild(menu);

        var items = [];

        var ignore_mouseup = null;
        function open_menu(e)
        {
            var show_menu = false;
            for(var index=0; index != items.length; ++index)
            {
                var item = items[index];
                if(item.show(e))
                {
                    item.item.style.display = "block";
                    show_menu = true;
                }
                else
                {
                    item.item.style.display = "none";
                }
            }

            if(show_menu)
            {
                ignore_mouseup = true;
                menu.style.left = (e.clientX + 1) + "px";
                menu.style.top = (e.clientY - 5) + "px";
                menu.style.visibility = "visible";
                e.stopPropagation();
                e.preventDefault();
            }
        }

        function close_menu()
        {
            menu.style.visibility = "hidden";
        }

        function contextmenu(e)
        {
            open_menu(e);
        }

        function mousemove(e)
        {
            ignore_mouseup = false;
        }

        function mouseup(e)
        {
            if(ignore_mouseup)
            {
                ignore_mouseup = false;
                return;
            }
            close_menu();
        }

        function keydown(e)
        {
            if(e.key == "Escape" || e.key == "Esc" || e.keyCode == 27)
            {
                close_menu();
            }
        }

        canvas.addEventListener("contextmenu", contextmenu);
        canvas.addEventListener("mousemove", mousemove);
        document.addEventListener("mouseup", mouseup);
        document.addEventListener("keydown", keydown);

        var module = {};
        module.add_item = function(label, show_callback, choose_callback)
        {
            var wrapper = document.createElement("div");
            wrapper.innerHTML = "<li class='toyplot-context-menu-item' style='background:#eee; color:#333; padding:2px 20px; list-style:none; margin:0; text-align:left;'>" + label + "</li>"
            var item = wrapper.firstChild;

            items.push({item: item, show: show_callback});

            function mouseover()
            {
                this.style.background = "steelblue";
                this.style.color = "white";
            }

            function mouseout()
            {
                this.style.background = "#eee";
                this.style.color = "#333";
            }

            function choose_item(e)
            {
                close_menu();
                choose_callback();

                e.stopPropagation();
                e.preventDefault();
            }

            item.addEventListener("mouseover", mouseover);
            item.addEventListener("mouseout", mouseout);
            item.addEventListener("mouseup", choose_item);
            item.addEventListener("contextmenu", choose_item);

            menu.appendChild(item);
        };
        return module;
    })(modules["toyplot/root"],modules["toyplot/canvas"]);
modules["toyplot/io"] = (function()
    {
        var module = {};
        module.save_file = function(mime_type, charset, data, filename)
        {
            var uri = "data:" + mime_type + ";charset=" + charset + "," + data;
            uri = encodeURI(uri);

            var link = document.createElement("a");
            if(typeof link.download != "undefined")
            {
              link.href = uri;
              link.style = "visibility:hidden";
              link.download = filename;

              document.body.appendChild(link);
              link.click();
              document.body.removeChild(link);
            }
            else
            {
              window.open(uri);
            }
        };
        return module;
    })();
(function(tables, context_menu, io, owner_id, key, label, names, columns, filename)
        {
            tables.store(owner_id, key, names, columns);

            var owner = document.querySelector("#" + owner_id);
            function show_item(e)
            {
                return owner.contains(e.target);
            }

            function choose_item()
            {
                io.save_file("text/csv", "utf-8", tables.get_csv(owner_id, key), filename + ".csv");
            }

            context_menu.add_item("Save " + label + " as CSV", show_item, choose_item);
        })(modules["toyplot/tables"],modules["toyplot/menus/context"],modules["toyplot/io"],"t81a655794c954831b08cff7175db3762","vertex_data","graph vertex data",["x", "y"],[[-7.0, -7.0, -1.0, -7.0, -6.0, -1.0, -1.0, 0.0, -1.0, 0.0, -6.0, -6.0, -2.0, -6.0, -5.0, -2.0, -2.0, -1.0, -2.0, -1.0, -5.0, -5.0, 0.0, -5.0, -4.0, -1.0, -1.0, 0.0, -1.0, 0.0, -1.0, -1.0, 0.0, -1.0, 0.0, -4.0, -4.0, 0.0, -4.0, -3.0, -3.0, -3.0, -1.0, -3.0, -2.0, -1.0, -1.0, 0.0, -1.0, 0.0, -2.0, -2.0, 0.0, -2.0, -1.0, -1.0, -1.0, 0.0, -1.0, 0.0], [9.0859375, 11.5, 11.5, 6.671875, 6.671875, 11.5, 12.0, 12.0, 11.0, 11.0, 6.671875, 8.5, 8.5, 4.84375, 4.84375, 8.5, 9.5, 9.5, 7.5, 7.5, 4.84375, 6.0, 6.0, 3.6875, 3.6875, 9.5, 10.0, 10.0, 9.0, 9.0, 7.5, 8.0, 8.0, 7.0, 7.0, 3.6875, 5.0, 5.0, 2.375, 2.375, 2.375, 3.5, 3.5, 1.25, 1.25, 3.5, 4.0, 4.0, 3.0, 3.0, 1.25, 2.0, 2.0, 0.5, 0.5, 0.5, 1.0, 1.0, 0.0, 0.0]],"toyplot");
(function(tables, context_menu, io, owner_id, key, label, names, columns, filename)
        {
            tables.store(owner_id, key, names, columns);

            var owner = document.querySelector("#" + owner_id);
            function show_item(e)
            {
                return owner.contains(e.target);
            }

            function choose_item()
            {
                io.save_file("text/csv", "utf-8", tables.get_csv(owner_id, key), filename + ".csv");
            }

            context_menu.add_item("Save " + label + " as CSV", show_item, choose_item);
        })(modules["toyplot/tables"],modules["toyplot/menus/context"],modules["toyplot/io"],"t81a655794c954831b08cff7175db3762","edge_data","graph edge data",["source", "target"],[[0, 1, 0, 3, 5, 6, 5, 8, 10, 11, 10, 13, 15, 16, 15, 18, 20, 21, 20, 23, 25, 26, 25, 28, 30, 31, 30, 33, 35, 36, 35, 38, 40, 41, 40, 43, 45, 46, 45, 48, 50, 51, 50, 53, 55, 56, 55, 58], [1, 2, 3, 4, 6, 7, 8, 9, 11, 12, 13, 14, 16, 17, 18, 19, 21, 22, 23, 24, 26, 27, 28, 29, 31, 32, 33, 34, 36, 37, 38, 39, 41, 42, 43, 44, 46, 47, 48, 49, 51, 52, 53, 54, 56, 57, 58, 59]],"toyplot");
})();</script></div></div>



<div class="toyplot" id="t806863d323164df980295a2a6ed17148" style="text-align:center"><svg class="toyplot-canvas-Canvas" height="300.0px" id="t74b9206545654da5a26c0a811869554b" preserveAspectRatio="xMidYMid meet" style="background-color:transparent;fill:rgb(16.1%,15.3%,14.1%);fill-opacity:1.0;font-family:Helvetica;font-size:12px;opacity:1.0;stroke:rgb(16.1%,15.3%,14.1%);stroke-opacity:1.0;stroke-width:1.0" viewBox="0 0 300.0 300.0" width="300.0px" xmlns="http://www.w3.org/2000/svg" xmlns:toyplot="http://www.sandia.gov/toyplot" xmlns:xlink="http://www.w3.org/1999/xlink"><g class="toyplot-coordinates-Cartesian" id="t52b4ab5dce9543c4a481ad48815685e7"><clipPath id="t75fd91ebf759450ea478367370355a7a"><rect height="300.0" width="300.0" x="0.0" y="0.0"></rect></clipPath><g clip-path="url(#t75fd91ebf759450ea478367370355a7a)"><g class="toyplot-mark-Text" id="t08f48f744bed4605b5c8313e2788fa2a"><g class="toyplot-Series"><g class="toyplot-Datum" transform="translate(224.40440894345812,56.716417910447767)"><text style="fill:rgb(16.1%,15.3%,14.1%);fill-opacity:1.0;font-family:helvetica;font-size:12.0;font-weight:normal;opacity:1.0;stroke:none;vertical-align:baseline;white-space:pre" x="15.0" y="3.066">3L_0</text></g><g class="toyplot-Datum" transform="translate(224.40440894345812,73.677069199457264)"><text style="fill:rgb(16.1%,15.3%,14.1%);fill-opacity:1.0;font-family:helvetica;font-size:12.0;font-weight:normal;opacity:1.0;stroke:none;vertical-align:baseline;white-space:pre" x="15.0" y="3.066">3K_0</text></g><g class="toyplot-Datum" transform="translate(224.40440894345812,90.637720488466769)"><text style="fill:rgb(16.1%,15.3%,14.1%);fill-opacity:1.0;font-family:helvetica;font-size:12.0;font-weight:normal;opacity:1.0;stroke:none;vertical-align:baseline;white-space:pre" x="15.0" y="3.066">3I_0</text></g><g class="toyplot-Datum" transform="translate(224.40440894345812,107.59837177747627)"><text style="fill:rgb(16.1%,15.3%,14.1%);fill-opacity:1.0;font-family:helvetica;font-size:12.0;font-weight:normal;opacity:1.0;stroke:none;vertical-align:baseline;white-space:pre" x="15.0" y="3.066">3J_0</text></g><g class="toyplot-Datum" transform="translate(224.40440894345812,124.55902306648576)"><text style="fill:rgb(16.1%,15.3%,14.1%);fill-opacity:1.0;font-family:helvetica;font-size:12.0;font-weight:normal;opacity:1.0;stroke:none;vertical-align:baseline;white-space:pre" x="15.0" y="3.066">2H_0</text></g><g class="toyplot-Datum" transform="translate(224.40440894345812,141.51967435549525)"><text style="fill:rgb(16.1%,15.3%,14.1%);fill-opacity:1.0;font-family:helvetica;font-size:12.0;font-weight:normal;opacity:1.0;stroke:none;vertical-align:baseline;white-space:pre" x="15.0" y="3.066">2G_0</text></g><g class="toyplot-Datum" transform="translate(224.40440894345812,158.48032564450475)"><text style="fill:rgb(16.1%,15.3%,14.1%);fill-opacity:1.0;font-family:helvetica;font-size:12.0;font-weight:normal;opacity:1.0;stroke:none;vertical-align:baseline;white-space:pre" x="15.0" y="3.066">2F_0</text></g><g class="toyplot-Datum" transform="translate(224.40440894345812,175.44097693351426)"><text style="fill:rgb(16.1%,15.3%,14.1%);fill-opacity:1.0;font-family:helvetica;font-size:12.0;font-weight:normal;opacity:1.0;stroke:none;vertical-align:baseline;white-space:pre" x="15.0" y="3.066">2E_0</text></g><g class="toyplot-Datum" transform="translate(224.40440894345812,192.40162822252375)"><text style="fill:rgb(16.1%,15.3%,14.1%);fill-opacity:1.0;font-family:helvetica;font-size:12.0;font-weight:normal;opacity:1.0;stroke:none;vertical-align:baseline;white-space:pre" x="15.0" y="3.066">1D_0</text></g><g class="toyplot-Datum" transform="translate(224.40440894345812,209.36227951153325)"><text style="fill:rgb(16.1%,15.3%,14.1%);fill-opacity:1.0;font-family:helvetica;font-size:12.0;font-weight:normal;opacity:1.0;stroke:none;vertical-align:baseline;white-space:pre" x="15.0" y="3.066">1C_0</text></g><g class="toyplot-Datum" transform="translate(224.40440894345812,226.32293080054276)"><text style="fill:rgb(16.1%,15.3%,14.1%);fill-opacity:1.0;font-family:helvetica;font-size:12.0;font-weight:normal;opacity:1.0;stroke:none;vertical-align:baseline;white-space:pre" x="15.0" y="3.066">1B_0</text></g><g class="toyplot-Datum" transform="translate(224.40440894345812,243.28358208955225)"><text style="fill:rgb(16.1%,15.3%,14.1%);fill-opacity:1.0;font-family:helvetica;font-size:12.0;font-weight:normal;opacity:1.0;stroke:none;vertical-align:baseline;white-space:pre" x="15.0" y="3.066">1A_0</text></g></g></g><g class="toyplot-mark-Graph" id="t07fd74e628894b8587242b7e17568b76"><g class="toyplot-Edges"><path d="M 50.0 122.438941655 L 50.0 71.5569877883" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 50.0 71.5569877883 L 119.761763577 71.5569877883" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 50.0 122.438941655 L 50.0 173.320895522" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 50.0 173.320895522 L 84.8808817887 173.320895522" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 119.761763577 71.5569877883 L 119.761763577 56.7164179104" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 119.761763577 56.7164179104 L 224.404408943 56.7164179104" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 119.761763577 71.5569877883 L 119.761763577 86.3975576662" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 119.761763577 86.3975576662 L 154.642645366 86.3975576662" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 84.8808817887 173.320895522 L 84.8808817887 139.399592944" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 84.8808817887 139.399592944 L 119.761763577 139.399592944" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 84.8808817887 173.320895522 L 84.8808817887 207.2421981" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 84.8808817887 207.2421981 L 119.761763577 207.2421981" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.642645366 86.3975576662 L 154.642645366 73.6770691995" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.642645366 73.6770691995 L 224.404408943 73.6770691995" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.642645366 86.3975576662 L 154.642645366 99.118046133" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.642645366 99.118046133 L 189.523527155 99.118046133" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 119.761763577 139.399592944 L 119.761763577 124.559023066" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 119.761763577 124.559023066 L 224.404408943 124.559023066" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 119.761763577 139.399592944 L 119.761763577 154.240162822" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 119.761763577 154.240162822 L 154.642645366 154.240162822" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 119.761763577 207.2421981 L 119.761763577 192.401628223" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 119.761763577 192.401628223 L 224.404408943 192.401628223" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 119.761763577 207.2421981 L 119.761763577 222.082767978" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 119.761763577 222.082767978 L 154.642645366 222.082767978" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 189.523527155 99.118046133 L 189.523527155 90.6377204885" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 189.523527155 90.6377204885 L 224.404408943 90.6377204885" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 189.523527155 99.118046133 L 189.523527155 107.598371777" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 189.523527155 107.598371777 L 224.404408943 107.598371777" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.642645366 154.240162822 L 154.642645366 141.519674355" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.642645366 141.519674355 L 224.404408943 141.519674355" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.642645366 154.240162822 L 154.642645366 166.960651289" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.642645366 166.960651289 L 189.523527155 166.960651289" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.642645366 222.082767978 L 154.642645366 209.362279512" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.642645366 209.362279512 L 224.404408943 209.362279512" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.642645366 222.082767978 L 154.642645366 234.803256445" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 154.642645366 234.803256445 L 189.523527155 234.803256445" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 189.523527155 166.960651289 L 189.523527155 158.480325645" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 189.523527155 158.480325645 L 224.404408943 158.480325645" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 189.523527155 166.960651289 L 189.523527155 175.440976934" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 189.523527155 175.440976934 L 224.404408943 175.440976934" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 189.523527155 234.803256445 L 189.523527155 226.322930801" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 189.523527155 226.322930801 L 224.404408943 226.322930801" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 189.523527155 234.803256445 L 189.523527155 243.28358209" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path><path d="M 189.523527155 243.28358209 L 224.404408943 243.28358209" style="fill:none;stroke:rgb(16.1%,15.3%,14.1%);stroke-linecap:round;stroke-opacity:1.0;stroke-width:2"></path></g><g class="toyplot-Vertices"><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="50.0" cy="122.43894165535957" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="50.0" cy="71.556987788331085" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="119.76176357738325" cy="71.556987788331085" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="50.0" cy="173.32089552238807" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="84.880881788691624" cy="173.32089552238807" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="119.76176357738325" cy="71.556987788331085" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="119.76176357738325" cy="56.716417910447767" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="224.40440894345812" cy="56.716417910447767" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="119.76176357738325" cy="86.397557666214396" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.64264536607487" cy="86.397557666214396" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="84.880881788691624" cy="173.32089552238807" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="84.880881788691624" cy="139.39959294436909" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="119.76176357738325" cy="139.39959294436909" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="84.880881788691624" cy="207.24219810040705" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="119.76176357738325" cy="207.24219810040705" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.64264536607487" cy="86.397557666214396" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.64264536607487" cy="73.677069199457264" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="224.40440894345812" cy="73.677069199457264" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.64264536607487" cy="99.118046132971529" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="189.5235271547665" cy="99.118046132971529" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="119.76176357738325" cy="139.39959294436909" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="119.76176357738325" cy="124.55902306648576" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="224.40440894345812" cy="124.55902306648576" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="119.76176357738325" cy="154.24016282225239" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.64264536607487" cy="154.24016282225239" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="119.76176357738325" cy="207.24219810040705" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="119.76176357738325" cy="192.40162822252375" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="224.40440894345812" cy="192.40162822252375" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="119.76176357738325" cy="222.08276797829038" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.64264536607487" cy="222.08276797829038" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="189.5235271547665" cy="99.118046132971529" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="189.5235271547665" cy="90.637720488466769" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="224.40440894345812" cy="90.637720488466769" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="189.5235271547665" cy="107.59837177747627" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="224.40440894345812" cy="107.59837177747627" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.64264536607487" cy="154.24016282225239" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.64264536607487" cy="141.51967435549525" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="224.40440894345812" cy="141.51967435549525" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.64264536607487" cy="166.96065128900952" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="189.5235271547665" cy="166.96065128900952" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.64264536607487" cy="222.08276797829038" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.64264536607487" cy="209.36227951153325" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="224.40440894345812" cy="209.36227951153325" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="154.64264536607487" cy="234.80325644504748" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="189.5235271547665" cy="234.80325644504748" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="189.5235271547665" cy="166.96065128900952" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="189.5235271547665" cy="158.48032564450475" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="224.40440894345812" cy="158.48032564450475" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="189.5235271547665" cy="175.44097693351426" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="224.40440894345812" cy="175.44097693351426" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="189.5235271547665" cy="234.80325644504748" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="189.5235271547665" cy="226.32293080054276" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="224.40440894345812" cy="226.32293080054276" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="189.5235271547665" cy="243.28358208955225" r="0.0"></circle></g><g class="toyplot-Datum" style="fill:rgb(40%,76.1%,64.7%);fill-opacity:1.0;opacity:1.0;stroke:rgb(40%,76.1%,64.7%);stroke-opacity:1.0"><circle cx="224.40440894345812" cy="243.28358208955225" r="0.0"></circle></g></g></g></g></g></svg><div class="toyplot-behavior"><script>(function()
{
var modules={};
modules["toyplot/tables"] = (function()
    {
        var tables = [];

        var module = {};

        module.store = function(owner, key, names, columns)
        {
            tables.push({owner: owner, key: key, names: names, columns: columns});
        }

        module.get_csv = function(owner, key)
        {
            var csv = "";
            for(var i = 0; i != tables.length; ++i)
            {
                var table = tables[i];
                if(table.owner != owner)
                    continue;
                if(table.key != key)
                    continue;

                csv += table.names.join(",") + "\n";
                for(var i = 0; i != table.columns[0].length; ++i)
                {
                  for(var j = 0; j != table.columns.length; ++j)
                  {
                    if(j)
                      csv += ",";
                    csv += table.columns[j][i];
                  }
                  csv += "\n";
                }
                return csv;
            }
        }

        return module;
    })();
modules["toyplot/root/id"] = "t806863d323164df980295a2a6ed17148";
modules["toyplot/root"] = (function(root_id)
    {
        return document.querySelector("#" + root_id);
    })(modules["toyplot/root/id"]);
modules["toyplot/canvas/id"] = "t74b9206545654da5a26c0a811869554b";
modules["toyplot/canvas"] = (function(canvas_id)
    {
        return document.querySelector("#" + canvas_id);
    })(modules["toyplot/canvas/id"]);
modules["toyplot/menus/context"] = (function(root, canvas)
    {
        var wrapper = document.createElement("div");
        wrapper.innerHTML = "<ul class='toyplot-context-menu' style='background:#eee; border:1px solid #b8b8b8; border-radius:5px; box-shadow: 0px 0px 8px rgba(0%,0%,0%,0.25); margin:0; padding:3px 0; position:fixed; visibility:hidden;'></ul>"
        var menu = wrapper.firstChild;

        root.appendChild(menu);

        var items = [];

        var ignore_mouseup = null;
        function open_menu(e)
        {
            var show_menu = false;
            for(var index=0; index != items.length; ++index)
            {
                var item = items[index];
                if(item.show(e))
                {
                    item.item.style.display = "block";
                    show_menu = true;
                }
                else
                {
                    item.item.style.display = "none";
                }
            }

            if(show_menu)
            {
                ignore_mouseup = true;
                menu.style.left = (e.clientX + 1) + "px";
                menu.style.top = (e.clientY - 5) + "px";
                menu.style.visibility = "visible";
                e.stopPropagation();
                e.preventDefault();
            }
        }

        function close_menu()
        {
            menu.style.visibility = "hidden";
        }

        function contextmenu(e)
        {
            open_menu(e);
        }

        function mousemove(e)
        {
            ignore_mouseup = false;
        }

        function mouseup(e)
        {
            if(ignore_mouseup)
            {
                ignore_mouseup = false;
                return;
            }
            close_menu();
        }

        function keydown(e)
        {
            if(e.key == "Escape" || e.key == "Esc" || e.keyCode == 27)
            {
                close_menu();
            }
        }

        canvas.addEventListener("contextmenu", contextmenu);
        canvas.addEventListener("mousemove", mousemove);
        document.addEventListener("mouseup", mouseup);
        document.addEventListener("keydown", keydown);

        var module = {};
        module.add_item = function(label, show_callback, choose_callback)
        {
            var wrapper = document.createElement("div");
            wrapper.innerHTML = "<li class='toyplot-context-menu-item' style='background:#eee; color:#333; padding:2px 20px; list-style:none; margin:0; text-align:left;'>" + label + "</li>"
            var item = wrapper.firstChild;

            items.push({item: item, show: show_callback});

            function mouseover()
            {
                this.style.background = "steelblue";
                this.style.color = "white";
            }

            function mouseout()
            {
                this.style.background = "#eee";
                this.style.color = "#333";
            }

            function choose_item(e)
            {
                close_menu();
                choose_callback();

                e.stopPropagation();
                e.preventDefault();
            }

            item.addEventListener("mouseover", mouseover);
            item.addEventListener("mouseout", mouseout);
            item.addEventListener("mouseup", choose_item);
            item.addEventListener("contextmenu", choose_item);

            menu.appendChild(item);
        };
        return module;
    })(modules["toyplot/root"],modules["toyplot/canvas"]);
modules["toyplot/io"] = (function()
    {
        var module = {};
        module.save_file = function(mime_type, charset, data, filename)
        {
            var uri = "data:" + mime_type + ";charset=" + charset + "," + data;
            uri = encodeURI(uri);

            var link = document.createElement("a");
            if(typeof link.download != "undefined")
            {
              link.href = uri;
              link.style = "visibility:hidden";
              link.download = filename;

              document.body.appendChild(link);
              link.click();
              document.body.removeChild(link);
            }
            else
            {
              window.open(uri);
            }
        };
        return module;
    })();
(function(tables, context_menu, io, owner_id, key, label, names, columns, filename)
        {
            tables.store(owner_id, key, names, columns);

            var owner = document.querySelector("#" + owner_id);
            function show_item(e)
            {
                return owner.contains(e.target);
            }

            function choose_item()
            {
                io.save_file("text/csv", "utf-8", tables.get_csv(owner_id, key), filename + ".csv");
            }

            context_menu.add_item("Save " + label + " as CSV", show_item, choose_item);
        })(modules["toyplot/tables"],modules["toyplot/menus/context"],modules["toyplot/io"],"t07fd74e628894b8587242b7e17568b76","vertex_data","graph vertex data",["x", "y"],[[-5.0, -5.0, -3.0, -5.0, -4.0, -3.0, -3.0, 0.0, -3.0, -2.0, -4.0, -4.0, -3.0, -4.0, -3.0, -2.0, -2.0, 0.0, -2.0, -1.0, -3.0, -3.0, 0.0, -3.0, -2.0, -3.0, -3.0, 0.0, -3.0, -2.0, -1.0, -1.0, 0.0, -1.0, 0.0, -2.0, -2.0, 0.0, -2.0, -1.0, -2.0, -2.0, 0.0, -2.0, -1.0, -1.0, -1.0, 0.0, -1.0, 0.0, -1.0, -1.0, 0.0, -1.0, 0.0], [7.125, 10.125, 10.125, 4.125, 4.125, 10.125, 11.0, 11.0, 9.25, 9.25, 4.125, 6.125, 6.125, 2.125, 2.125, 9.25, 10.0, 10.0, 8.5, 8.5, 6.125, 7.0, 7.0, 5.25, 5.25, 2.125, 3.0, 3.0, 1.25, 1.25, 8.5, 9.0, 9.0, 8.0, 8.0, 5.25, 6.0, 6.0, 4.5, 4.5, 1.25, 2.0, 2.0, 0.5, 0.5, 4.5, 5.0, 5.0, 4.0, 4.0, 0.5, 1.0, 1.0, 0.0, 0.0]],"toyplot");
(function(tables, context_menu, io, owner_id, key, label, names, columns, filename)
        {
            tables.store(owner_id, key, names, columns);

            var owner = document.querySelector("#" + owner_id);
            function show_item(e)
            {
                return owner.contains(e.target);
            }

            function choose_item()
            {
                io.save_file("text/csv", "utf-8", tables.get_csv(owner_id, key), filename + ".csv");
            }

            context_menu.add_item("Save " + label + " as CSV", show_item, choose_item);
        })(modules["toyplot/tables"],modules["toyplot/menus/context"],modules["toyplot/io"],"t07fd74e628894b8587242b7e17568b76","edge_data","graph edge data",["source", "target"],[[0, 1, 0, 3, 5, 6, 5, 8, 10, 11, 10, 13, 15, 16, 15, 18, 20, 21, 20, 23, 25, 26, 25, 28, 30, 31, 30, 33, 35, 36, 35, 38, 40, 41, 40, 43, 45, 46, 45, 48, 50, 51, 50, 53], [1, 2, 3, 4, 6, 7, 8, 9, 11, 12, 13, 14, 16, 17, 18, 19, 21, 22, 23, 24, 26, 27, 28, 29, 31, 32, 33, 34, 36, 37, 38, 39, 41, 42, 43, 44, 46, 47, 48, 49, 51, 52, 53, 54]],"toyplot");
})();</script></div></div>
