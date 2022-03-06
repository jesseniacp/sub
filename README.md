
# Visualizacion de archivos  netCDF - Humedad Relativa 
*ALUMNOS* |  
----------------------| 
CASAS POMACAJA JESSENIA | 
IIlan Prada Catheling Palmira |
Perez Rojas Naason |
Sangama López Sofia Samantha |
Zevallos Segura Percy Miguel |

-  Instalando libreria netCDF
```
!pip install netCDF4

Requirement already satisfied: netCDF4 in c:\users\armando\anaconda3\lib\site-packages (1.5.7)
Requirement already satisfied: cftime in c:\users\armando\anaconda3\lib\site-packages (from netCDF4) (1.5.0)
Requirement already satisfied: numpy>=1.9 in c:\users\armando\anaconda3\lib\site-packages (from netCDF4) (1.16.5)
```

- importar las librerias que se usaran 
```
from netCDF4 import Dataset 
import numpy as np 
import matplotlib.pyplot as plt
```
- leer el archivo netCDF4
``` 
ncFile = Dataset("C:/Users/ARMANDO/Desktop/datosnetCDF/humedadcolor.nc",'r')
```
- para ver las propiedades del archivo
```
print(ncFile)
<class 'netCDF4._netCDF4.Dataset'>
root group (NETCDF4_CLASSIC data model, file format HDF5):
    Conventions: COARDS
    title: mean daily NMC reanalysis (2011)
    description: Data is from NMC initialized reanalysis
(4x/day).  These are the 0.9950 sigma level values.
    platform: Model
    history: Sat Mar  5 16:04:28 2022: ncrcat -O -d lat,-90.000000,90.000000 -d lon,0.000000,357.500000 -d time,2011-01-01T00:00:0.0,2020-01-01T00:00:0.0 -n 10,4,1 /Datasets/ncep.reanalysis.dailyavgs/surface/rhum.sig995.2011.nc /Public/www/X179.6.218.238.63.16.4.27.nc
created 2011/01 by Hoop (netCDF2.3)
Converted to chunked, deflated non-packed NetCDF4 2014/09
    dataset_title: NCEP-NCAR Reanalysis 1
    References: https://www.psl.noaa.gov/data/gridded/data.ncep.reanalysis.html 
    NCO: netCDF Operators version 4.8.1 (Homepage = http://nco.sf.net, Code = http://github.com/nco/nco)
    dimensions(sizes): lat(73), lon(144), time(3288)
    variables(dimensions): float32 lat(lat), float32 lon(lon), float64 time(time), float32 rhum(time,lat,lon)
    groups: 
```
- Ver las variables
```
ncFile.variables
OrderedDict([('lat', <class 'netCDF4._netCDF4.Variable'>
              float32 lat(lat)
                  units: degrees_north
                  long_name: Latitude
                  standard_name: latitude
                  axis: Y
                  actual_range: [ 90. -90.]
              unlimited dimensions: 
              current shape = (73,)
              filling on, default _FillValue of 9.969209968386869e+36 used),
             ('lon', <class 'netCDF4._netCDF4.Variable'>
              float32 lon(lon)
                  units: degrees_east
                  long_name: Longitude
                  standard_name: longitude
                  axis: X
                  actual_range: [  0.  357.5]
              unlimited dimensions: 
              current shape = (144,)
              filling on, default _FillValue of 9.969209968386869e+36 used),
             ('time', <class 'netCDF4._netCDF4.Variable'>
              float64 time(time)
                  long_name: Time
                  delta_t: 0000-00-01 00:00:00
                  avg_period: 0000-00-01 00:00:00
                  standard_name: time
                  axis: T
                  units: hours since 1800-01-01 00:00:0.0
                  actual_range: [1849584. 1928472.]
              unlimited dimensions: time
              current shape = (3288,)
              filling on, default _FillValue of 9.969209968386869e+36 used),
             ('rhum', <class 'netCDF4._netCDF4.Variable'>
              float32 rhum(time, lat, lon)
                  long_name: mean Daily relative humidity at sigma level 995
                  units: %
                  precision: 2
                  least_significant_digit: 0
                  GRIB_id: 52
                  GRIB_name: RH
                  var_desc: Relative humidity
                  dataset: NCEP Reanalysis Daily Averages
                  level_desc: Surface
                  statistic: Mean
                  parent_stat: Individual Obs
                  missing_value: -9.96921e+36
                  valid_range: [-25. 125.]
                  actual_range: [  0. 100.]
              unlimited dimensions: time
              current shape = (3288, 73, 144)
              filling on, default _FillValue of 9.969209968386869e+36 used)])
```
- Dimensiones
```
ncFile.dimensions
OrderedDict([('lat',
              <class 'netCDF4._netCDF4.Dimension'>: name = 'lat', size = 73),
             ('lon',
              <class 'netCDF4._netCDF4.Dimension'>: name = 'lon', size = 144),
             ('time',
              <class 'netCDF4._netCDF4.Dimension'> (unlimited): name = 'time', size = 3288)])
```
- Variable rhum
```
ncFile.variables["rhum"]
<class 'netCDF4._netCDF4.Variable'>
float32 rhum(time, lat, lon)
    long_name: mean Daily relative humidity at sigma level 995
    units: %
    precision: 2
    least_significant_digit: 0
    GRIB_id: 52
    GRIB_name: RH
    var_desc: Relative humidity
    dataset: NCEP Reanalysis Daily Averages
    level_desc: Surface
    statistic: Mean
    parent_stat: Individual Obs
    missing_value: -9.96921e+36
    valid_range: [-25. 125.]
    actual_range: [  0. 100.]
unlimited dimensions: time
current shape = (3288, 73, 144)
filling on, default _FillValue of 9.969209968386869e+36 used
```

- Definimos las variables que vamos a trabajaar air(time, lat, lon)
```
rhum = ncFile.variables["rhum"][:]
lon = ncFile.variables["lon"][:]
lat = ncFile.variables["lat"][:]
t = ncFile.variables["time"][:]
```
- Llamamos a las variables 
```
lon
masked_array(data=[  0. ,   2.5,   5. ,   7.5,  10. ,  12.5,  15. ,  17.5,
                    20. ,  22.5,  25. ,  27.5,  30. ,  32.5,  35. ,  37.5,
                    40. ,  42.5,  45. ,  47.5,  50. ,  52.5,  55. ,  57.5,
                    60. ,  62.5,  65. ,  67.5,  70. ,  72.5,  75. ,  77.5,
                    80. ,  82.5,  85. ,  87.5,  90. ,  92.5,  95. ,  97.5,
                   100. , 102.5, 105. , 107.5, 110. , 112.5, 115. , 117.5,
                   120. , 122.5, 125. , 127.5, 130. , 132.5, 135. , 137.5,
                   140. , 142.5, 145. , 147.5, 150. , 152.5, 155. , 157.5,
                   160. , 162.5, 165. , 167.5, 170. , 172.5, 175. , 177.5,
                   180. , 182.5, 185. , 187.5, 190. , 192.5, 195. , 197.5,
                   200. , 202.5, 205. , 207.5, 210. , 212.5, 215. , 217.5,
                   220. , 222.5, 225. , 227.5, 230. , 232.5, 235. , 237.5,
                   240. , 242.5, 245. , 247.5, 250. , 252.5, 255. , 257.5,
                   260. , 262.5, 265. , 267.5, 270. , 272.5, 275. , 277.5,
                   280. , 282.5, 285. , 287.5, 290. , 292.5, 295. , 297.5,
                   300. , 302.5, 305. , 307.5, 310. , 312.5, 315. , 317.5,
                   320. , 322.5, 325. , 327.5, 330. , 332.5, 335. , 337.5,
                   340. , 342.5, 345. , 347.5, 350. , 352.5, 355. , 357.5],
             mask=False,
       fill_value=1e+20,
            dtype=float32)
lat
masked_array(data=[ 90. ,  87.5,  85. ,  82.5,  80. ,  77.5,  75. ,  72.5,
                    70. ,  67.5,  65. ,  62.5,  60. ,  57.5,  55. ,  52.5,
                    50. ,  47.5,  45. ,  42.5,  40. ,  37.5,  35. ,  32.5,
                    30. ,  27.5,  25. ,  22.5,  20. ,  17.5,  15. ,  12.5,
                    10. ,   7.5,   5. ,   2.5,   0. ,  -2.5,  -5. ,  -7.5,
                   -10. , -12.5, -15. , -17.5, -20. , -22.5, -25. , -27.5,
                   -30. , -32.5, -35. , -37.5, -40. , -42.5, -45. , -47.5,
                   -50. , -52.5, -55. , -57.5, -60. , -62.5, -65. , -67.5,
                   -70. , -72.5, -75. , -77.5, -80. , -82.5, -85. , -87.5,
                   -90. ],
             mask=False,
       fill_value=1e+20,
            dtype=float32)
t
masked_array(data=[1849584., 1849608., 1849632., ..., 1928424., 1928448.,
                   1928472.],
             mask=False,
       fill_value=1e+20)
```
- Elegimos el tiempo que vamos a trabajar
```
data = rhum[3287,:,:]
```
-
```
x,y=np.meshgrid(lon,lat)
```
-Codigos para el grafico
```
fig=plt.figure()
    ax=fig.add_axes([1,1,1.5,1.5])
    cmap = plt.cm.get_cmap("jet")
    ax.set_xlabel(r'Lon',size=15)
    ax.set_ylabel(r'Lat',size=15)
    
    subR=[-60,10,240,360]
    ax.set_ylim(subR[0],subR[1])
    ax.set_xlim(subR[2],subR[3])
    cmap = plt.cm.get_cmap('jet')
    ax.set_xlabel(r'Lon',size=12)
    ax.set_ylabel(r'Lat',size=12)
    ax.grid(b=True,which='major',color='grey',linestyle='--',alpha=0.4)
    
    
   
    mapaf=plt.contourf(x,y,data ,20,alpha=0.9, cmap=cmap)
    mapac = plt.contour(x,y,data ,10 ,colors='g')
    plt.clabel(mapac,fontsize=10,inline=1,fmt='%1.1f')
    plt.colorbar(mapaf)
    plt.title("HUMEDAD RELATIVA ENERO/2020")
    plt.show()
 ```
 - Imagen 
 
 ![Humedad Relativa en enero 2020](https://github.com/jesseniacp/sub/blob/main/humedad2jupyter.jpeg) 
 ```
