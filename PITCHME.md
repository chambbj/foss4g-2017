---

### Point Cloud Filters & Pipelines in PDAL
#### FOSS4G 2017, 18 August 2017

<span style="color:gray">Bradley J Chambers, DigitalGlobe</span>

---

### Overview

  - Python Package
  - Docker Images
  - IPython/Jupyter Examples
  - Status of PCL Filters
  - Filter-only Pipelines

---

### Python Package

  - The PDAL Python package can be installed via pip.

    ```console
    pip install pdal
    ```

  - Once installed, simply

    ```python
    import pdal
    ```

---

### Docker Image

  - Existing PDAL image (`pdal/pdal:latest`) approaches 4 GB
  - Plugins on top of PDAL base image grow even larger

+++

| **Image** | **Tag** | **Size** |
|---------|-------|--------|
| pdal/dependencies | 1.5 | 3.1GB |
| pdal/dependencies | latest | 3.31GB |
| pdal/pdal | 1.5 | 3.67GB |
| pdal/pdal | latest | 3.67GB |

+++

  - Prototype Alpine image with ~80% of the plugins

| **Image** | **Tag** | **Size** |
|---------|-------|--------|
| pdal/dependencies | alpine | 1.07GB |
| pdal/pdal | alpine | 365MB |

---

$$\sum_{i=0}^n i^2 = \frac{(n^2+n)(2n+1)}{6}$$

---

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
kuQvhBAJ6P8HxbTec3YHrFoAAAAASUVORK5CYII=
"
>
</div>

</div>

</div>
</div>

</div>

---

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[78]:</div>



<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
        font-size: 20%;
    }

    .dataframe thead th {
        text-align: left;
        font-size: 20%;
    }

    .dataframe tbody tr th {
        vertical-align: top;
        font-size: 20%;
    }
    .dataframe tbody tr td {
        vertical-align: top;
        font-size: 20%;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>X</th>
      <th>Y</th>
      <th>Z</th>
      <th>Intensity</th>
      <th>ReturnNumber</th>
      <th>NumberOfReturns</th>
      <th>ScanDirectionFlag</th>
      <th>EdgeOfFlightLine</th>
      <th>Classification</th>
      <th>ScanAngleRank</th>
      <th>UserData</th>
      <th>PointSourceId</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>38010.000000</td>
      <td>3.801000e+04</td>
      <td>38010.000000</td>
      <td>38010.000000</td>
      <td>38010.0</td>
      <td>38010.0</td>
      <td>38010.0</td>
      <td>38010.0</td>
      <td>38010.000000</td>
      <td>38010.0</td>
      <td>38010.0</td>
      <td>38010.0</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>512767.010570</td>
      <td>5.403708e+06</td>
      <td>356.171434</td>
      <td>0.426835</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.146330</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>std</th>
      <td>38.570375</td>
      <td>8.587360e+01</td>
      <td>29.212680</td>
      <td>0.494624</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.989249</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>min</th>
      <td>512700.870000</td>
      <td>5.403547e+06</td>
      <td>295.250000</td>
      <td>0.000000</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>512733.530000</td>
      <td>5.403645e+06</td>
      <td>329.060000</td>
      <td>0.000000</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>512766.940000</td>
      <td>5.403705e+06</td>
      <td>356.865000</td>
      <td>0.000000</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>2.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>512799.900000</td>
      <td>5.403790e+06</td>
      <td>385.860000</td>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>2.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>max</th>
      <td>512834.760000</td>
      <td>5.403850e+06</td>
      <td>404.080000</td>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>2.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
