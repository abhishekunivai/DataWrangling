In this exercise, we will learn how to merge dataframes, merging them on the index, concatenation along axes, combining/joining data with overlaps, reshaping and pivoting. 

We will also study various data cleaning techniques including removing duplicates, replacing values, renaming axis indexes, discretization and binning, detecting and filtering outliers. We will work on transforming data using a function, mapping, permutation and random sampling, and computing indicators/dummy variables. 


```
import pandas as pd
import numpy as np
```

#2.0 Combining dataframes



Concatenating objects



```
"""
In the dataset below, the first column contains information about student identifier and 
the second column contains their respective scores in any subject. 
The structure of the dataframes is same in both cases. We would need to concatenate both of them.
""" 
dataFrame1 =  pd.DataFrame({'StudentID': [1, 3, 5, 7, 9, 11, 13, 15, 17, 19, 21, 23, 25, 27, 29], 'Score' : [89, 39, 50, 97, 22, 66, 31, 51, 71, 91, 56, 32, 52, 73, 92]})
dataFrame2 =  pd.DataFrame({'StudentID': [2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30], 'Score': [98, 93, 44, 77, 69, 56, 31, 53, 78, 93, 56, 77, 33, 56, 27]})


```


```
# We can do that by using Pandas concat() method. 

dataframe = pd.concat([dataFrame1, dataFrame2], ignore_index=True)
dataframe.head(20)
```





  <div id="df-ed78793a-e24c-4621-b698-a2e96b77e417">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>StudentID</th>
      <th>Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>89</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3</td>
      <td>39</td>
    </tr>
    <tr>
      <th>2</th>
      <td>5</td>
      <td>50</td>
    </tr>
    <tr>
      <th>3</th>
      <td>7</td>
      <td>97</td>
    </tr>
    <tr>
      <th>4</th>
      <td>9</td>
      <td>22</td>
    </tr>
    <tr>
      <th>5</th>
      <td>11</td>
      <td>66</td>
    </tr>
    <tr>
      <th>6</th>
      <td>13</td>
      <td>31</td>
    </tr>
    <tr>
      <th>7</th>
      <td>15</td>
      <td>51</td>
    </tr>
    <tr>
      <th>8</th>
      <td>17</td>
      <td>71</td>
    </tr>
    <tr>
      <th>9</th>
      <td>19</td>
      <td>91</td>
    </tr>
    <tr>
      <th>10</th>
      <td>21</td>
      <td>56</td>
    </tr>
    <tr>
      <th>11</th>
      <td>23</td>
      <td>32</td>
    </tr>
    <tr>
      <th>12</th>
      <td>25</td>
      <td>52</td>
    </tr>
    <tr>
      <th>13</th>
      <td>27</td>
      <td>73</td>
    </tr>
    <tr>
      <th>14</th>
      <td>29</td>
      <td>92</td>
    </tr>
    <tr>
      <th>15</th>
      <td>2</td>
      <td>98</td>
    </tr>
    <tr>
      <th>16</th>
      <td>4</td>
      <td>93</td>
    </tr>
    <tr>
      <th>17</th>
      <td>6</td>
      <td>44</td>
    </tr>
    <tr>
      <th>18</th>
      <td>8</td>
      <td>77</td>
    </tr>
    <tr>
      <th>19</th>
      <td>10</td>
      <td>69</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-ed78793a-e24c-4621-b698-a2e96b77e417')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-ed78793a-e24c-4621-b698-a2e96b77e417 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-ed78793a-e24c-4621-b698-a2e96b77e417');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




### 2.0.1 Exercise 
The argument ignore_index creates new index and its absense keeps the original indices. 
Note that we combined the dataframes along axis=0 which would combine together the dataframes along same direction. What if we want to combine both the dataframes side by side?


```
# Hint: Try to change value of "axis" argument
#Insert Your Code Here

#Solution: pd.concat([dataFrame1, dataFrame2], axis=1)
```

### 2.0.2 Exercise
Write a Pandas program to join the two given dataframes along rows and assign all data.



![image.png](data:image/png;base64,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)

![image.png](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAbAAAACuCAYAAABX5Vh1AAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAADsMAAA7DAcdvqGQAAEvpSURBVHhe7b0PTFtXvu/7nZeRXPXquZpKRqmENZOEZm6g0wnuNL5GUTFqC7ze4EwbH3c0hlZlSE88pDfOtZphaDMeplMek5RCCgxtIPQkrm9bH3JyYvoqTF5fzCgyh9sTgzpxojakmtRoWrGlRvGoFZZS+f3W3tv/wAZMMNhkfdBm7728vL32+vdbv99ae/++FyHA4XA4HE6e8X/Iew6Hw+Fw8gouwDgcDoeTl+SvAJvowebNm9EzIZ+vJ9bzvXE4HM4KseICLPihHZY9/fDL5+uJfLu3rKQ3NAVPVxOMFZtFIVu+pwk9I1MIyx9zOBzOarHiAky45oBnYn12Z/l2byue3mk3rI9XwtLhgv+6FBSccKF9XyXMAwEpgMPhcFYJPgfGWTr3FuJ+XQPaTo/jyuef43PaJp02aOgj/1vDGONqGIfDWUWWIMBCmBrpQdOectFktFlbifo2N6ZC8scMec6GbcYOFtAOo3we3SxDghiVIQxZxLB5czzydRLjSshpMFdCK15Pi8rfuuTP5kJxh1pRX60Vr6Wtrof95BiE7+SPZaQ0WOH5Kjl+eX0r3NcSeuIM7y1zMrg3wQ93VxNq5bRurjDCctgB/w35c8Zy0ruU6zLu1qCxsxmmUhUUcpCSBJrteToQpiDMjS8SRuB4LbTaWipvLuE4HM7KsYgAo86ntx6V+9rhmghKQdRReY9bUXlytWaCQhhrk9MwRp2kGCZg6jM5PUmE4e+iuAf64f1MjvmZF44WM3YdcmP+N67h/cPJ8YPeflh/2b1K2kQm9ybA3WKEtcMFn5xWXPfD47TD2NCP5RvwVuq6BVDeLR8mEYC3zQdB8KH9XS/dMYfD4awQ7EHm9FyMdG/aFNn0++HIzVk56NZs5Av/+5FX37kkByRz8Q2Kv6mbvpmeGfc+irMp0u2XA6L4u8Xwfe4ZOSASmfW9FtlBYY+8+H7k0tfRRMxGbp5/bd41Zun7uyhsz5HzkS++iQbORHx/fo6usSPymi/6/XgaNlH4c3/2RWZuUeCtmxHf67vE8Nc+luIlspR7y4RM7o1SHBl+ozty1v9FZJallUH3dv7IHvEeuj+RwxJYWnozv24S3/gir+7YFNnx8vnITTkomdnIpbfMkR07zJT/qWNwOBzOclhEA1NAUUy7T3zwXpfHzhsUUJea0Gwukc6zCmkoH/ZAUDWi7RUTSn4QNVwpoLznLvk4TuDCKQSKm9Hyoh7qqDagUEFn2Q8TaRquySk5MI7mYC96LTqoNtDJBiV0+moxfOpLWRvJGpndG6BC1QuNMJSqoWBpZdC96R+roANK6y0pKHNu57qk8b7Vin4Y8NI/66GUQ5NRoOT5dzA+/g5sutQxOBwOZzksIsBKUHekGfppB6zV26GttqJ10INAtvv2GDcxw1a7PXw/iqL9e1oETH9KCbvcipo5cz6bNxvRw2L8XZhnwqrYqYnN56wumdybjDAGx2FLbAm7uO1plz+8DZZ1XRJevb+CpUsB25t/gqFQDuZwOJxVYtFFHIriBgz4JjEy0IbdD07Dc8iCGq0Wtb1+6sKyTQjCp/LhuiPDe2NL2HeZYXd6YkvYV4RlXZe0x6NmGI/O4hnXABpL12YIwOFw7myWsAqR2KBEkd6E5iODGL0yil5zAXxHX8fZtB3eDEIZz9aHEfj4onwcpQDqh2n3txm6YiI0+r9wXj6OooSKaQE72zAqL/Get72SzsyVCcu5t1Rkcm9AYKQPbkEFQ+sQJq8m3NNpmxwjHQunN+PrfheE+1ANzL2A7bQTjT/jZkEOh7M2LCzAvvKgp8sN/3Qorm19vwBbfsokxVUIKTpGlaqM/jvw/lAAoTlL16OoCh8Q98Mer7S8/TsBY70W1Ld5xfA4KmzRlACX+9B3Jiil4UYA7hYa/XfMXQWpQInGBFxoh73Xi6kbK68fLuXelk4m90Zi7Ru2HpCEXqEaSjZX9V0YwQk3ek6ke5xgaenN6LrfTsF1yAjrqFoSXkvSvPgyeg6Hkx0WdqfylRuWMis88mkSpc0YOt2AeUs5LvfDuKt13uuLqo6No7dGJZ2Ex9D+iBk9c+bSNI/qEf7Ii8LEuCRErbstpCVIpxIa1NkrMNPSjgdOf04dqRwM0g5s1MGeST1JZ0uIy54D0x7wJIWJsOeo9rQnpzfKUu4tEzK4t5DXjsfrHWxZRTIqFVSCgGfm3gdjCenN5LrRPEvLE50Y7zaQaE7Ej57NRogzasZeTB6pWgEtmMPhcBbTwDYa8AdnC+qe0EAtB6lLq6iDdWLclUJ4MdicmYu+82jRnI4sAYUO+/9XJxr00lVVW/VoODaCgWN7oRNDEthYhT+93YY6Oa5aX4cW1wBaqqIpSkQNw5EP4LTXoao01ee3yVLuLRMyuDelvhnOYw3Qb5V+WbW1DKamAYw6XhLfhJGSJaR3WdfNiBLom8pEbbDxSR0XXhwOZ8XgDi05HA6Hk5csbREHh8PhcDg5BtfAVoyEuZ5FsWHw88YVMtFxOBzOnQnXwDgcDoeTl3ANjMPhcDh5CdfAOBwOh5OXcAHG4XA4nLyECzAOh8Ph5CVcgHE4HA4nL+ECjMPhcDh5CRdg6xxhpAnlm7WoPR6Iv5CZw+Fw1gFcgM2Fvcx382b0TMjneY2AMbcLQdr72rxg751fMusqHzgczrLI8X4gbwRY8EM7LHv6571ZfT2QvXtTQWcwQU17vV2f+uXLHA6Hk6fkjQATrjngWaf+pLJ5b6pK5uBzHAPPloD7TeZwOOsJbkLkcDgcTl6yhgIshKmRHjTtKRdtrJu1lahvc2Mq0cuzbH9lm7GDBbTDKJ9HN8tQ3BUjc7jIwubZa+XrJMaVkNNgroRWvJ4Wlb9N5+GY4g61or5aK15LW10P+8kxyaN0AlIarPB8lRy/vL4V7msJWlaG95YZ7MXCydfa3LWQgTKTfOBwssuS21AUwQ93VxNq5XibK4ywHHbAf0P+nMGc89JnzCu4/3i9uLCpstkDAUF4/1hL9V6L2l7/nIVOS2vzWWEZ6Q1d98Jx2AJjhdTmtdW1aOryYOpbOUKU2LXpOBSA6zC7Pn2H+mDryQDd9WIwx8EsT7SwngnKYTLMu/5JeyzPWFk0Hc9enq2RAAsj0FuPyn3tcE3IGSBMwXvcisqTqzXLFcJYm5yGsSnZI7GAqc/mFIgIVaIuinugH97P5JifUWVpMWPXITcV51yu4X2qFInxg95+WH/ZjbHsWApvg0zygcNZLZbahgS4W4ywdrjgk+Phuh8epx3Ghv55C5eC/9YKS5tXXNg09d6/o6+NOtsBH50J8B3tI6EpR8y4zWeHpafXD0cFCVinB/7rUojwmQ+uDgvM/7c3pVCaueyC9fEaNDnZ9Qnqg90tNWgdWUiEUX9x9CAJLsBwbBCdTyY63xXgObQL5hZHLM9YWbjazPjdh/L5SsNe5rv6XIx0b9oU2fT74cjNWTno1mzkC//7kVffuSQHJHPxDYq/qZu+mZ4Z9z6KsynS7ZcDovi7xfB97hk5IBKZ9b0W2UFhj7z4fuTS19FEzEZunn9t3jVm6fu7KGzPkfORL76JBs5EfH9+jq6xI/KaL/r9eBo2Ufhzf/ZFZm5R4K2bEd/ru8Tw1z6W4iWylHtbPnJev5H66pnkA4ezGmTWhmYiw290R876v4jMsngMapvnj+wRv9/9iRz25dnIPvmaB9xfRCIfS/V706ZddD2q757fiOfR+p5Jm88KGaY3ErkUOfXbU5HzUzep9cp8fSny/v/cQfEORIbjXV/CtTdFdjR0R3xfyt8Ivi+F/89hylUZue+UfmeW+iqWr49EfvP/UJrmIl/X/C+XEsriZuTq+b5ItycxASvHGmlgCiiKafeJD97rsrTfoIC61IRm82qslaNRxIc9EFSNaHvFhJIfRJc3KKC85y75OE7gwikEipvR8qIe6rvlQIUKOst+mGjU4ZqckgPjaA72oteig2oDnWxQQqevFsOnvszSSGRZZJYPHM5qsrQ2pELVC40wlKqhYPEY1Db1j1XQAcW7JQXF0NtgqyGtYYNUv1VmG/b+jOq7KlGTWF6bzwpLTC9QgrrWOui3KOOLtX5Qggo98zoYRjiFCU/1ZCcG+xqh2yh/o7AC/9cTtA+nMhORRtr7K1g6BJi630HbE3N/n7hbiQLaXb3ghf9rKQgKJYr0DWisVMkBK8saCTDK7CPN0E87YK3eDm21Fa2DHgRWrW+/iRmmZj98P4oWXZonYPpTStjlVtQwm27SZkQPi/F3YZ6KXrFTkwer/jLJBw5ndVlyGxLGkuZ+xG1PateyVU9WILHr1ewogVI+jrO8Np8NlpZeidBnHvQcqkWlNp5e7QGP/Ol8NHpd0rXZYMDQ/Tk+7zbQUTJX37XDctQHzZE0wouh1KOhrw7qj9phpjSU19vRPzSGYBYzas0WcSiKGzDgm8TIQBt2PzgNzyELarSpJlKzQQjCp/LhHQ3PB06eM+2GdZc5ae7nTiQ80YP6agvaB32YyoIicP8TJjxTCnh6euCZlgNToH60BYNXxjF4jBSUDWPoO2BG+fZyNH2YnVnDNVyFSGxg6qUJzUcGMXplFL3mAviOvo6zaSviDEIZS/MwAh9flI+jFED9MO3+NkNXTITU5Avn5eMoSqgKabeTPU9Fo5NU2yv6tKOipbOce7tdMskHDif3CIz0wS2Q5tA6hMmrCW3ytE2OsRxWq82vFCGM/Vs7/NCgcWAcVxLSOX6sSo5zm9xD1z7WCxNcsBzogX/uysZEFCpoahrQ0jeC8YuDaNYH4drvyMoCtrURYF+Rqtvlhn86FNe2vl+ALT9lteYqhBQduUpVRv8deH8ogFCaJZmqwgfE/bDHKy3bZEs6ey2ob/OK4XFU2KIpAS73oe9MUErDjQDcLWYYO+auglSgRGMCLrTD3uvF1I2VL4Wl3Ft2yCQfOJzcI/wNW2dIA7FCNZRsDuy7MIITbvScuJ3HQLLf5leWMELiIwMqqDfJc2DhEKa8DrS/t4LtuLAKbY5OGKbbYdmbQoj91YGmk5RfQkJ+3V2Ekp+wdQ3ZGaCvkQYWxqUOK4yPbMe2qG35/m2oPOQBSvdC/xM5WgLqB/U0viAV9nANtt8ft/EmPStVTKMEFY3KjtdDy+Lcr4X5qJfU2vmvUSp5Yj8MKgFuW7mUhodqYD0J1NltmDtmUVY2ovNJwHu0HpUPbYv9dnS73feELeneMiHhGTNmsxdnAzqMKa+bST5wOLlG0U/qqNsOoOeZ7VL9pn6kfI8V7R/PzpvHyYRst/mVRYXih8UeBE0Vclq3bUdlvR3nV3qtSaEBf3rTBvUYCbHDcx4nuBWCq4XyS5uQX5QOc1cAKvPPocvCOo61EWAbDfiDswV1T2hik4jq0irqNJ0YdzWkfmcfmzNz0XceLUpfMRU67P9fnWjQS1dVbdWj4dgIBo7thU4MSWBjFf70dhvq5LhqfR1aXANoqUo1QamG4cgHcNrrUFWaZgLzdljKvWWLjPKBw8ktlPpmOI81QL9VajmqrWUwNQ1g1PGSOChcPllu8ytM0bMDGGwyQfND6Zz1pw1HBvFB5zNSwAqiKG1ExzEDcMaKWlI6YkKstA4jJNxMumg/pkKRzgTbmyM4lyWT6/fYWnr5mMPhcDicvGFtF3FwOBwOh7NMuAaW87D3GsrzWItiw+DnjbdpOuFwOJz8gGtgHA6Hw8lLuAbG4XA4nLyEa2AcDofDyUu4AONwOBxOXsIFGIfD4XDyEi7AOBwOh5OXcAHG4XA4nLyECzAOh7OqCCNNKN+sRe3xQPxl3hzOMuACjMPJGPZwefzFruLWxd/evzQEjLldCNLe1+YFe5f87SAMWcT8z62X63JWiyUIsBCmhlpRX62VGmqFEU3HxyR3JZzchbmSOWmHZU+5VG7aStQfdsB7fWGfBsEhK7Ryp7yqncIy07seCX7I8qGfxOTiZBJ35UkhyGObBe6v5GhJqKAzmKCmvd4+30sEZ5UQvVizN8ezstKicq8djv9M09ZY2zzeFPN4ra2uR+vQVHqP1DcC8HRZSMum+Fke2C0iwMLwd9FNHuiH9zPZBcd1P1xtZuw6NOdV+pzc4VvqWExamFsc8EzIpSRMweu0o77Ckb6zm3aj/Y9u6mNW+Z34y03vmqFBY8xp4CBux3ViKoRrLB+WZlzLJG6uoKpkjiLHMfBsieS7irOqMO/NRi3zYs18d7EQAVMfOWA3PQ77R3PFUhDuQ7tgbnPFPF4Ln3nRf4AGmCSckmqewGRDPcofqoGlI+Et9VlkQQEWnuiHvcMP1aM2OH1XpAY77oTtURWEM6+if97NcnKBwHt2tE/QCPdFJ0Yvxb2zXvnLINrqZYd386CK2vEq3IU2vPQ/VvdtistLLydnODgYK7P41gvDRvlzTk6hUKlRZGjGwLlJuayuYLTdQDqxAIdzOEnwCEOtsJ4RoHm2E0MXpbKdHO5EXSnp3x2tcFyWI5I+5n2DWee8mGXy4nTbqvgTXECAkfblaUeAkvHSK43QbZS7EZUOja+8RKF0s15/ejWSs2ZIXmo1+HmNDuq7pTCGolAD08t1Kc02waF2vHpGDdvvG6BbZV/py0kvQlPwdM03a8zTRWhU6KZ4tQkmcMth0upED7aJSOYw0dnnd0F4u6yyeaUc9W00mrwtk3myGZ6l1X5yjhk+wQmpsYMFtMMon0e3mCPSTOLGWEIaskqm84aU3pEeNCWalNvcmErZ4ZAmR91T0NsDq3x/5fWtcF9LpZkuNR+yWR/WmEID2joboN8SbegKqJ+0wbaTDr0C9exRgjj/rx6g2IbmJgNKfiCFKrca0PyyjXLdj7P/EZ3FVEJDgov5XzzXR/Livrvk8OyygACbgv8M7cxPQ584kmIu5/tJnWTHzgDF4uQaSqXknfXUu96ldVDTbrQecKOktQONP1l9fSfz9HrQtLsSlo65Zo12eJLmXQS4W4ywUjxfggnc47TD2NCfcgHBP748jx4TdVId1FmKX6HO67gFvz6x3OUG883wLK2OltU0w+dCGjIhjEAvpXdfO1yJJuXjJEROphJ69+DSv9TCWN8Ot3x/QW8/rL/sxliSDMs8H1a+PuQ4xYq4xUO4DN8FGh48pYcmoVsIfzUGxwmX2H4C/msxgafUN6K5pigrjivTwl7mm5Kb5yO/27QpsumNi9L5rZmI7619kUdYWGw7EBmekT7m5BDfXIr0NeyQyki/L9LtvhiZmZU/m8cXkbONFK/xLB1JzLj3id/t9ssB2Saj9M5I6d20I/Lcn32RL76Rg7/5InLxX09Fzn8pn4vMRIbf6I6c9X8Rmb0lB83ORM4f2SN+v/sTOUzkYqQ7Wq+f+l3kbOCmFHzTF3ntv1PYju7IJSlkDvL3ou1kDrP+7sgu+nzPkfPxtFIafH9+LrKD0vCab/6NXnyDpaObrrw4S4m7nDQsjYQ8m7tRfUrfNSycZ7HPfz8cuRlN2q3ZyBf+9yOvvpNcCtG6ysrT/Pp5qd7cuhnxvb5LDH/tYykeI7N8WG59yFP+9n7kOZY3JxLuKtAn5tc+t1ySN69Gzr5ipryS84Vt6fLhy7ORfezztGW8MqTXwL4NYYZ2GhKnTOWuLdPCzFTnH0pu+gdfKaNPwwjnsyq9Xrm7BA1950T33gaFH+0HjNBuY6aP+SaY4JlWWD82oLPJgDVznJ5BenH9PFwf0qjwhV70WhJMjneroTHWJVsLoELVC40wlKqh2CAHKVTQP1ZBBzRuvCUFJVFqw6CjBYZieRyp1KGCGfMp+nKWSgQunEKguBktL+rjaaU06Cz7YaKLuiazb8PIhTRkBmkBxbT7xBdfhbpBAXWpCc3m1OsWNQd7ceKgHiqmKWxQQqevFsOnvozqB8vMhxWuD7lJEO6jTfDSvTb/IiF/w6QJ065AcRNjpHWWb6+EdcAHMBOicxQDz9OHa5wP6QXY3UoU0M7fYhRVbp+gRlWTE+P/74CoJipCV+lTqmjRjoGTYyhRVNmIzuFxTJ6jMjMoEGAmmN1N8EzLUa67YLf5YXiZBEehHLZmLCG9RDg4BWpCqNZrlra4Q1wubInNlYnbngXcg+p10CTMwzE0L7DJ6+U4ChUw/Sm18MutqIn+dmwzoofF+LuA7M4jr0IaUi3i6GaLApZLCeqONEM/7YC1eju01Va0DnoQiMuieVTsXKw+LDMfVrQ+5CJBeA7VSoPYY3RPifeqUIjzz459lZLyoiqT5riGO9GguwthVh5UyEtqh1kivQBTSgKMpbCsvhMjk6PofV4HlSiwQmJhQ3U/Cld5xTUnc5RbSGvuJK2ZrTQiofW7d8fEUZPwyXl4qWG7D8gT5fKmPeARv9e+RzqfvyAgu6RLLyNMo8IlM+2GdRdbLuyJzZVx8gNFcQMGfJMYGWjD7genqZO1oEarRW3vnKXbnOXz7RRcNiMso6XoPN05fxB7bwGkIFl58b2TMMc1g+CntNtZJMuJtWGBRRxFKDGzfQXqGg0oSpyZuzGGYSftK0vWzuzEyRi14WmYaC9cz/aof2VIlV5lQYE4sr/46eJLDwIjfXALKhhahzB5NUE7OL3ST26lQwkV6wF2sueeEn4/cXtFn2bSewahJRfSQnFvJw1rzAbSyvUmNB8ZxOgVGkCbC+A7+jrOLmswksf5kA1CfvTsNaPpgi618GJs3IKHmCm3uA77Y8qLzOUxnL1MunJJ4W1o2rfPAgJMCY2+jhJHI+BD/fFlxzf86D/0OwpVofEJ3Z1T4HlDAP3WfnguBxFKGKqGQ0GMHe+jciPF+cdSpVPV9KZsyOPHpCc4bKel896abFbRpadXZKsGJjrxNh+EfSgQ/05YgH/QAW/CKkRpeX4B1IVqKFnj+y6M4IQbPSfYVVcDBUo0JIIvtMPe68XUjaXpDioVm1924H12f4vMMS8ed3lpWFO+8qCnyw3/dCiubX2/AFt+ynrZqxCWNfrKw3zIFqSAtD9nRPvfK9CbTniJlED3lEY0u9pbPAjKWRa+7oH9cCu1XD3qHk09J7lafI+t5JCPUxCEm1RM9iDbXDQHB+F8YYnzEJxVhD2/QpVTPptHaQOc/c3Qyc90pIK9X46ZEZkAayyVA7NG5ullbxIw72mXHuVIogqdvvgDtCGvHY/XO9g8czIqFVSCgGeS7k9OB5vPoXq9IOw5rAXm0aqOjScI/fRtiJEyjy/3w7irdd79JV9XZklxl5GGJZGlPPvKDUuZFZIhew6lzRg63SDOzTDS1lX595afDxncW57h74o+P5iGxHtmb8mpo3yY91o5FQzHBtFZE7fBRcsiLVnIywU0MIYahiMfwNlkguaHUohqq7QKcYASwoVXLqJBg48q1kETykqjlUuFIl0V6uwDGH17YeG1+mSeXkVpIwaGe2EzlqFI7pvYCjXbmzZUJaxCVOqb4TzWAP1WKZJqaxlMTXRNx0urOAEvtyF7Hapi97cIbP7H1UKj26K45pmOJcVdRhrWko0G/MFJ9/SEJjZFoS5l9cGJcVdceGVOnuVDLnC3Bo1vj6DzeX1SW2t2fpAkvNaKRTQwDofD4XByk0U0MA6Hw+FwchMuwDgcDoeTl3ABxuFwOJy8hAswDofD4eQlXIBxOBwOJy/hAozD4XA4eQkXYBwOh8PJS7gA43A4HE5ewgUYh8PhcPISLsA4nDxHGGlC+WYtao8H1szVSC6kgXPnwQUYhyPCXt4a94kmbl3zXxecewgYc7sQpL2vzSt60J1PJve2nHxYSho4nJVnaQIsTBX0ZBNqtVSZ97vnv92bk3t8x8rMDsse2VmlthL1hx1xF+0xUnRY0W21yzo0BU8X1bNqrfT7FUY0dXkwtSz3GfkFe5P35s0WuBPcwSQjldN856Iq6AwmqGmvt+tv40W3t0MupIGTEaKn8npUsj6dNOfKvXY4/jNNQ2N9yfGmmFdzbXU9WoemUvsUzCTuCrDwy3xDQXjfa0frCTemou3miU6M35a7cE7WSesCgWHDYJI7dNYxUlz5LIlVLOvw5X5YnmuFN5XEXHWXFnKerOLvSq4okOQOJonwGFq3mRFM5VIlIzK5t9XPB072Se+OSIW6vnNoeTTRy2MmLrVW3/3WghpYYPDXqG8j4VVYh87hATTK4ZzcJvCenYQXjYZfdGL0UtxR5ZW/DKKtXpmyEjG/SdF4sW21BiokcLsPMeHF0jyAkYvy71+9gtHTbWi4d/077lHdV0T/PQh+KZ3P44ZA3QNQdB8fOnJuD4VKjSJDMwbOTcptndpZO2vrAhzOYbGeRRGGWkWBpHm2E0Nyu5wc7kRdKQ1vOlrhuCxHJDKJu1IsKMBK/psJpibmg6cFhq1K3CWHc3IbyROxBj+v0UF9txTGUBRqYHq5LudMPMEPu9FDlVtzsBe9Fj2Kov6/Nigk30PmOSkW/HDPMTVaDjviXsNjMA1CNrt9F4S3yyqbTMppYEbCYhFvxwuy5DQskQ1La113xdy6S/cm/nZ0W/U5uwzTsJQ8Y84s6bOeiTD8x+vFhSGVzR7qWqn8/lgLLVso0uufs1AkhKmRHjQlmsvZwDuV3Uo2rdcvUm6SSdcKz1d0beqYo/HL61vhvpbny1QKDWjrbIB+S1TTonb2pA22nXToFRKmDYI4/68eoNiG5iYDSuR2qdxqQPPLNupH/Dj7H9EZz0zirhwLz4EV16HteR1UsUbDyQeUSmbu8eDUu14It9NJrwoCJrxe2puwt3YpJgYB7hYjrB0u+D6Tm9p1PzxOO4wN/SkXEPzjy/PoMZHQ6oiawqkzPG7Br08st0FlnoZFUSjEgcVstLyuu1C7uRau6/J5eBb/oBgULU/JLM+C/9YKS5uXSkrA1Hv/jr42EjoDPjoT4DvaR4JFjkiiLNBbj8p97XBNyLqDMEXlS4OVk3OFaRDuQ7tgbnHAOzcN1Va4p6WgONfwPpsnOtAfix/09sP6y26MrdellsWKeBsULsN3gRSZp/TQJNS78FdjcJxwiWUW8F+jEiEyibuC8FWI65Cif2pB86Mq+Klhax+zoGfID2GRBuc5II9ISTsxPtMkfWdVhF+QNDDa7dSgeImeohU/tqHz9CiuXJVNjVfGMWAhoT3RB+9f5UgJ+Nqa0I46dH4gm0wmnWgspgZ1Yvkr5jJNw6LcW4BC2k19KTVx4ZPz8NGfe0zulL+mjptiFNwrnTINu5H9rrgNwiaHri6ZpSGTPHM5h6E7NorPXWziwoP+4wIaXVcw+aZJPI+bWgPwHiVB9WwvJq/I101jeg4O2ueZuFganC/qoRLcePXdsTmaHV37o6Boih9nab46CecLNMwQeuBbThnnMtfHMEwCSPOULm6hEYIkwklhUxVI56EpuEkLfqTMjNYP5Xr5cRAzbJ9J3BWEC7D1yN0laOg7h5E3bTAo/Gg/YIR2GzObpTGrJBGE/4JL/M6uQ246WyWUdy3RRK1C1QuNMJSqoYhaBhQq6B+roAPq/G9JQUmU2jDoaIGhWDaZKHWoqKI9RV/eQHoZaciIEAL/24OqJ6poVDux4qPWtSHDPNPbYGMu62XTqspsw96fKaBUzXVjTxoDDUbwiS++wjal6TmIMTdp+sXNaLHHTVwsDTpLC2x6SkWvf96ARjJry1aoDUro9NVieHSgsT4gzfRoE7zUTpp/kZBnYdJuaVeguImx4xaUb6+ElbRgMLOgcxQDz9OH0TaUSdwVhAuwdYsSRZWN6Bwex+S5ATQbFAgws8ruJniSTCWJo2g2yryC8XO9aCyl+nbGiv6PsrUAdg6k7c3Kh4siLgG2xJbqituelOsoJfQ6aBLmAhmaF9j9Jq7GzJBM07AYGwvBlnHgFsuFKQRG6vD0rypQ9uFFBKgIwt/cpPAiFKZaoZgvZJBnVU9WIFFUaXaUUI1ORQnqjjRDP+2AtXo7tNVWtA56EJgnXwQIpGGgShPXMGKoUbKThV7C9JzHGCp2rvzKudwiCM+hWlg/NqDzGLWHxHYim7Ud+yphZnPGqjI0HBvBueFONOjuYk9XsXGJlD+ZxF1BuAC7A1Bu0aOhcwSDbKXRdRd+N89UkgCNXlVbqmD7rbTmdObblR4zzUUFFZs89lzEtaXIymk3rLvMsDs98Efnh1abLKWB6RqeaWrpl/0Y1jyELaUl0Bc74PskjNANpgvn8TKqLJaborgBA75JjAy0YfeD09QhW1CjTbXYYzFIm7uT5vu/nYLLZoRltBSdpzthYDbsRGSzNhPwVWwxn+8dNNcUyQOJGQQ/pd3OIohGw0ziriBcgN1BqA1Pg80gCNeFRR8sDH0tDWGz36DVKHqYLQ134FTUVr4AgZE+uAUVDK1DmIzOpbDt9OrNAmUnDbIpjAh+4gUe3sL0AmiqVOi/4Je008QJ9jwj6+W2QYkivQnNRwYxemUUveYC+I6+jrMxYSnnr2e+mZBpIYELFFr8AArvlKcUQn707DWj6YIutfBibNyCh1ieFddh/9zFfJfHcPYy6b8lhUyxyizuCsIF2LojgH5rPzyXgwglDD/DoSDGjvfBRceqHy9QkcIhTHl7YD1MMVV1+Lku+y1aY7BBT3tvcy0sx8cQ/FYKx3dhBCdcaHXGuxzpEYECqAvVULJGIsZxo+cEu7PVITtpKEDBj2j3t7Pof+cqqkn7YpSU7gbODMPDFi38iOKIoflH1srtKw96utzwT4fi2tb3C7Dlp6xHvgohNlIrgc5AeXq5Ffaj3ngdCwvwdvwW7TRmSFrAsJ65MYb254xo/3sFetMJLxHKs6c0Up61eBCUMzh83QP74VbqafSoezSaY5nEXTkWfhPHRM/Cdn3+Vo4cRH57gnw2j9IGOPuboYtOYqcrY1UZbG+eQGPp6oz5g0NWGA+keXVVwpsgQl47Hq93zI+nUkElCHjm9Ofi/J2EnBdLeZPEInWdPegdfQNGZmlYKgLc+7WwshWZoDK6QmXEsj7khX17PemnRGJ7yyC9uRB3yXnGngMrswLR78q/EbuWfG6bE98jXmwOpc0YOt0QF0oLvKFGpbOhty8+ByS9GcUT/50oc9OTh/i7NsPYIZ+kIrG9pM0z0qaPDaKTLbSJkkncFYJrYOsODRp8VFkOmlBWGq0wKhTpqlBnH8Do2wnCKwWqrWUwHezF0PA71HBXz2ClrunEueFe2IxlKJL7hWhaRp6NCx+lvhnOYw3Qb5UiiXGa6L4cLy1/QUaGZCcNKhT+WD40l6EkmvVKDSrM8vFCmnOOk7Vy22jAH5wtqHtCg2htV5eyus5ewJAgvBh3a9D49gh6qW1ofigFqbaSZkBxPzg1ZwEDR0LOs87n9bF2Ka7wdH4wXyBlEneFWFgD43A4HA4nR+EaGIfD4XDyEi7AOBwOh5OXcAHG4XA4nLyECzAOh8Ph5CVcgHE4HA4nL+ECjMPhcDh5CRdgHA6Hw8lLuADjcDgcTl7CBRiHw+Fw8hIuwDgcDoeTl3ABxuFwOJy8ZHEBFpqCp6sp5kW1fE8TekamVtw1NGeF+U7A2Ek7LHvKJc+32krUH3bE3a6nQBhzofVQLSq1UY+5PfDLn3GWA3sbfjQv5Y3KofZQK1xjKd+7n1WCH7L60L8GZRqE28LuX4ueOW8qD4+1Q8vr2tpwI0B9uwXlLP+7Fsj9G344DtfL/YIWleYm9Kerv3O9bov1vR/Zqu4LCzDmRfXxSlg6XDEvqsw/UztzGz0Q99HEyTGYWwOTFuYWBzwTspNIYQpepx31FY75HQXzzHqoHFpWMQd9mFr9vvXOgcrBN9iPJrMWxhYvde2rh3CN1Ye1GHoKCHrAPKfg1IXE2heG/4JrvosVTnYR/HC11aP8oRrq2z0L10EmA6qNsDu9cr8gYIoNdM27YB2a882vPPO9bov1vRXmXVZ4vpLDVpCFBdi9hbhf14C20+O4IntQnXTaRPcH/reGMcbVsJwk8J4d7RMq6F90YvRS3Pvtlb8Moq1eOcerL3Uibx1E0+AsyurbMPiXyVhZf/5546q5KFnXMD9e0Ty9MolRZzOqfkht6GQ9WofunO57t9GU7BE57KfOrQSNlio5gJN9QvC+YUTTcS9mH7XBeboN6XM/BM8bVrgFDRoH4jLgim8AjaUC3H90JcmAwIfdctxRXIl63ab6PtRqgEpw498/Xvm6vrAAY/5dOpthKlXFOj0lCTTb83RAklW4IYVxcgvJ+60GP6/RQZ3g40hRqIHp5bpkH0nXz6K7KwDNwV6ceNkETeFcAcdZURRKqKkN9f5Lm+iF2vPW2WQX9zQ6dnc1obZaK5lgKoywHCateU5bYw4XN29mo9oQpoZaUS/HL69vhftaQq/CHDCKJrqoE8N2GOXz6GaZJ0STr6mtrof95BiE7+SPl8k9FRV4RjiLscvSedjvg6v8aVT/V3Z2E+HEAbFsAo+mIV0+RM204j18F4S3yyqbuspR30baxbw0072N9KAp0bTe5sZUSst6dvJhbVFCQ4Kr4dgIzvU1QnffXXJ4CkJsgAGUNLXApo/LAMVGPWwv20go9cD3VzmQEZ6hf0V44KdqKJjXbQbV95KHH8L9dFhw98r3LLexiKMASu4ALidRKpne5MGpd72LNjbhk/Pwog77n9VwwbWa/LAaTxtpf/kirsVMKzSqbTHC2uGC7zNZqFz3w+O0w9jQnyzoRK7hfTY3caAfXjl+0NsP6y+7b8M6Qhp5V/I1hc+8cLSYseuQe3kmT0HAVbbfoIGudgZn/4PdiWQ+rHhMh5L7iug8mDAgDsJ9aJdoAo+mIZYP1aQRTEtBifzjy/PoMZHQ6iBhJH6FhNlxC359IjHXwgj00r3ta4cr0bR+nITeybmG9SzkQ46g1DeiuaaIRNkifBsCE0n3KFPEvE8tWmemvpTLhygp30thLlgamuAYC9KAJAxhwgX7ITt8pTaYdi76ixmTuQD71o/zZwCVuQKalU8PZwUo+qcWND+qgp8aq/YxC3qG/BDSdGjBv3mA4gLS/x2w7zdKE7psonYvjeQ/S7/gg3O7KFG4ibmtJS3hSymEofixDZ2nE00w4xiwUFcx0Qdv4mhXJADvR0HRVDzO4l+dhPMF0q8TR8aljdJ1aBs8yAJsGJTPo1uia/zwRD/sHX5oLANx8zOlwfki6YtnXoVrOZLxuzCJA4mSn5kw4w2QAAjAP1iBioepE9mQrAUEB+2wnhGgebYTQxeT08BMUa++Oxa7XhRfWxPplnXo/GBSij/pRGMx5dAJb4Lgp/w6SoLq2V5MXpGve/UKRk+3oeHe5OFbVvIh39hYiAeoavg6SOBfjvYFYYSmx+B4wyXOpfunmYiTKW6A84MWVH1NQstcjm3btkG7px3XSjsx8nZj3Mv4CpKhAGPzJa3ohwEv/bN+cQnOWRvuLkFD3zmMvGmDQeFH+wEjtNuYSWWuqUTA9Ke0u9yOerMdjg/98shSwNRHNJKvrke/bO7hrDwFhXNnGFWoeqERhtJEE4wK+scq6IBGurekoESY6bfXooOKxd+ghE5fLYYnjowzIXDhFALFzWihjjpmfqY06Cz7YaI0uCan5MDlodCUwfTpeUwMjeFUeQV0P5A/iBHEmNtLnSGlwW5ASfRzMQ3MlEU50ZswjxaFRviDjhYYiuVeSalDBZvcoWyIixoFFCTU8Ikvvhp3g0Jye29OMqxnPR/yAw0ML0vzV027tksm183bsP0RM+zv+VjWomCOUFLcV4KHStTyGYO07ytXMZ0leZ+BACPh1fsrWLoUsL35JxgK5WBOjqJEUWUjOofHMXluAM0GBQLMVLK7CZ55Jhg1qpoGMHLxijwqncTQsTqqvn60uuePdjkrg6j9ktDC96VzkbnLkNlGo9h0VOxcSdMvG9BQt3S5FTXR345tRvSwGH8XkLFeHp7FP+RDkmAoM/rx6h9PiebD+CCYBk+izBUgXKBdlSZ5rlZEjZKdLPQSpueuaNProJkzpaF5gWlOiQuRSlB3pBn6aQcNzrZDW21F66AHgXmyPkv5kIeoa/4EJw2ETTSoElEVQW9uwcAp0rTotFBVIIUz5BWLrR+rpUUfkyPorC8DxnpQvyarEGOEMHbUDOPRWTzjYitQ+GxJPqHcokdD5wgG22k0dd2F38VMMAoo2Qh3ZyOan9ej6AdyudJIvqSmAc+wGjp9ZzTU1SeIKfGZqGqU/FAMkDqAucuQ1wNfC/BRd6cWLZUKaHS7IQgkyB5MtOGQwEihYaaGNKmohpohiuIGDPgmMTLQht0PTsNzyIIarRa1pNXxgVoqFOJAuO30qDS4HR/BwCt10P+XEA05VHjgR1Hzcwjet9iKxRI09pyQFn0oi0iDewfOV5ja7Eb3h/NncW+XxQXYd2xCtQbmXsB22onGn3HDYb6iNjwNE+2F61GhpIRqE41oL/hxOcWK0tlv5APOihP+TxccXjowlsXmkgMjfdQBqGBoHcJkdA6MbadtUoQVYQahtCMSqg/MsrKzDaPR3567UWe07B5A1jQVO5vpWr0wbJTOk5HNfInL7WMEEbhAocUP0MhfDloONEAr0pvQfGQQo1dG0WsugO/o6zgbGzRkOR/yHpIJ75yCoHoGup/IQZhCwEm74t2o/lmyglP06M9FbS3gv8aGKSvKwgJMfMDVCOuoWhJeXPPKAwLot/bDczmIUMKQMhwKYux4H1x0rPpxITNciZT8t90oodC+NzyY+lYODAsY67Wj/QKg15fG4nJWgG+D8A+24leNPVRSGtjq4h2h9PhDAdSFaiiZhvFdGMEJN3pOsFK7fVSqMvrvwPtDAYRSrk5VoERDQ5wL7bD3ejF1Y5V0EgX9Lu1mxTSVQGegs8utsB/1IphQJ70dv0U7CX3NU7oU5sUl8JUHPV1u+KdDcW3r+wXY8lMmra5CiAn2NcqHXOfbkFgf2/eSTDgDGOymBPOsCqqdtLvsg5etQIzWr3AIAe//Jy74KNFsWfG+5HsRQj6eB3vWRHuA2enTwB7Q7DbwDi6nYM/FGJF21qS0Ac7+5oTJcwEe2y5YzswfG6l0zRgYaMjK6qE7g4XKQg1T9ztoeyI+4R3y2vF4vWP+KFVFnYMg4JnTn9MgUgqKtk1bQpgIe+5rTzuqjo0nrS4UudwP465WsTNJJDkuja5trINKPVae93tLQEor0OlLo3V95YalzApE08HeJFNH+TbntVMMlc6G3r7GhPkuOY8PDuLzF+YuipmD/Dspe7TSZgydproun2YjH3KFRfv1xLyU61MyKuhfHkBvfQmJ+jihj6j+7k1RfxkqA3rPdqIqpda9fDJchcjJfTRo8A2i86AJZdGJV6pwRboq1NkHMPp2ovBiqFB15AM4m2g0Jc/FqLbqKa4TH5ziwmulUZeWwXSwE4Pjo0nCi6HUN8N5rAH6rZIwUW2luE1UZo6XEka6twGb/3G1oO7RogUGnWoYWH2w16EqVn9WGfYChbdH0Et1eH6dTBReGbLRgD846f6f0NBdSqhLWbtwYtyVKLwYOZAPOUas7vr+goE5wouhfLQF54Z7YTPG81eswwd7MXJu5YUXY0ENjMPhcDicXIVrYBwOh8PJS7gA43A4HE5ewgUYh8PhcPISLsA4HA6Hk5dwAcbhcDicvIQLMA6Hw+HkJVyAcTgcDicv4QKMw+FwOHkJF2AcDofDyUu4AONwbgNhpAnlm7WoPR64o91x5EI+8LK48+ACjMNZNgLG3C4Eae9rS3Rdf6exlHxgL92d4xyya+5rhaNkEjcKL4s7kUUFWOgzD3oOGWlkwyqSFpXmJvSMTHEnh7nOd9SgT9ph2VMudQDaStQfdsRdqYsIcO9P6CRSbfvdFCs/YW/dZvfQM+et5uyt2VoKN1KneHsjdRV0BhPU7O3cdv3yXHzkEFJ+WeBO6zlXEiyWobk1IhfyYX2VRdYRPX/Xo1LL2jn163vtcPznAr36jQA8XRZJDiw0mLjhT74uyYv+sez1IIsIMEpMtQXtg34a2TAETI250L6POsMBPsbJWZg7CpMW5hYHPBNSyUGYgtdpR32Fg0r1Dmbajd81O4AnO9Hxwu2741dVMqeH4xh4dv7budcd4TBuyodzWTwfNGiMOYQcxMIuOjOJG+eOKovbIDzRA6OWef72YkqULdSvf+SA3fQ47B/NEWKCH662epQ/VANLh0eWA2lgHsWrjcnXJXnRat4F69CC31w2iwgwBZT1bRj8yxW5Mn2OK+d6UVdMou0trqbnKoH37GifoJHoi06MXop2BFR2fxlEW70yoXGrYOiOf560fdAsuvCoqtJRrPVCEO6OV+EutKH3FUPM5QNHQnVfEf2nTupL6XweNwSxAyu6b/3UiDsRhUqNIkMzBs5Nyu39CkbbmV9HAQ7ncIKQCsH7hhFNx72YfdQG5+k20bNyakLwvGGFW6DBx8A4rsj9yBXfABpLBbj/6MJYFiYmFxFgJah72QRNYbzLU2ypwu5H6UDFxzi5iuTZV4Of1+igTvCdpCjUwPRy3RLMK1Rx3+2DX9WIZyrXkfgiwW49o0bzK2l8StFo093VhNpqrWQ+rTDCcpg01hvy5zEynaMJYWqkB02J5tw2N6ZSWmwo7lAr6uU0aKvrYT85BmGeB+UEc953QXi7rLLZppyuTUIopcflRdhwl3ywMHcxb9Eiy5mrWmkyTMNSypg5vqTPeibC8B8n7YOZwpo91L1TPv+xFlq2UKT3ds3Pa0ihAW2dDdBvifoCV0D9pA025lHZK9B9RlFCQ4Kr4dgIzvU1QnffAvUj5IdvkCRGUwtselVskKzYqIftZRtUQg98f5UDV5DMFnEwF+djPeh+j0bu/1zF7cw5ilLJdCcPTr3rTdHxLYHLLnQ7BdLgTNCtk3FK+K89ONgcgOFYBxqK5cAkaJTYYoS1wwXfZ3ITvu6Hx2mHsaH/NqwNYQR661G5rx2uRHPucRI4J+d2tNRhdlHcA/3wymkQPvPC0WLGrkPulOabf3x5Hj0mElodJBDFr1Ane9yCX59YRoqTXPsT112o3VwL13X5PDyLf1AMipanZFbGwX9rhaXNSzkqYOq9f0dfmx31Az46E+A72gdP2rnCPKZYkWR+Veob0VxTRKJsEb4NYYZ29yhTxLxPLVpzpr6Mi8aVYgkCLGGi//5tKDefR1HrB+is4QaYXKXon1rQ/KgKfuo4tY9Z0DPkh7Dk4WJc+9q7Xsr4ph/9v28HDvbiTwvck+LHNnSeHsWVq7IZ9co4BizU9Cb64E0aPWYyRxOA9ygJqmd7MXlF/s7VKxg93YaGe5MlQXiiH/YOPzSWgbjpl9LgfFEPnHkVrhQ2GF9bE9pRh84PZHPQpBONJKADJ5Zh4r+3AIW0i3Y0wifn4aM/95gsOr+mjptiFNwrnS53rmplySwNSy9jwOUchu7YKD53NdKZB/3HBTS6rmDyTZN4ntbUmo9cH8PwBcrNp3TLU0w2FuIBFdXHDhqoXY6aFsIITY/B8YZLnHf3TzMRt7JkpoGJUGew14imD1ONBzk5wd0laOg7h5E3bTAo/Gg/YIR2GzMtpTNbJRDVvg6uH+3rfFcr2ifqsP/ZhRZtqFD1QiMMpWoooiYyhQr6xyrogDr0W1JQ5tCIlml8n/jiK0A3KKAuNaHZnNxVBC6cQqC4GS0ksGKmX0qDzrIfJkqDa3JKDkyg1IZBRwsMxfLIV6lDBZuooCTfnokrhMD/9qDqiSr4Lkywy60DMixjvQ02NuCRTasqsw17f6aAUrXeBu9BuI82wUt1qfkXy7WraWB42QCV4EbTru2yOXcbtj9ihv09prUCBVnoT5YgwBIn+mn08UEn6kqDcO0/iP7LchRODqJEUWUjOofHMXluAM0GBQLMbLW7CZ5pOco8otpXA/Ya1k8jrXjBhgaVA79pSW2GiyEuLbbAWCFbHNi2hzS326IEdUeaoZ92wFq9HdpqK1oHPQjMkwgCpj+lwMutqIn+dmwzoofF+LtAJTQHvW7efJ7mBdZWG0WzTUbQKJot48CtWfo3hcBIHZ7+VQXKPryIAP1w+Bu2BrEIhRtZpDwlgzKuerIiaaGPZkfJ4qa0vCMIz6FaWD82oPNYmrnhJaKu+ROcNGg20QBBRFUEvbkFA6daxMUfhaoCKXwFyVADo9FHsQEtR1pQRprYxWvrY1y23lFu0aOhcwSDbKXRdRd+9+5Y6tG5rH1p/nk3dLdRkXOOe3SwUcNSn7HiYLpnv9gS4F1sabEH/uiczwqhKG7AgG8SIwNt2P3gNHUYFtRoc3MhANM1PNNMkPoxrHkIW0pLoC92wPdJGKEbTPwvbaFHTpLFMs5Lvp2Cy2aEZbQUnac7YWD249tCIQ6a206PSgrP+AgGXqmD/r+ESFqo8MCPVn5B2DJMiITiHvyf8iEnf1Abngaz3gvXU4zkY9pXHfY/uf6W5yhKG9HRqoe/w4LfpHgmJTDSB7eggqF1CJPR+RG2nV6hmZ0NpBHrTWg+MojRK6PoNRfAd/R1nI11pEqoWAeykz3LlPD7idsr+ixrALK5kwh+4gUe3kIaSAk0VSr0X/CD6WVzJ/nziayXcT4R8qNnrxlNF3QrJLzSEYT7nVMQVM9A9xM5aAXJUIBJk3I9La/CAz0qHuTPg+QeAfRb++G5HEQoYXgfDgUxdrwPLjpW/biQxkNzkLWvkl+ZoP+BHLbOUP+iBZ1PAu4DrXDPMaNKjx4UQF2ohpLNj7AVtxNu9JxgOXYbfOVBT5cb/ulQXNv6fgG2/JT1GFchxEYSCpRoaHhxoR32Xi+mbqyFblaAgh/R7m9n0f/OVVST9sUoKd0NnBmGhy1a+BHFEUPzj6yVcb5xYwztzxnR/vcK9GZLeH0bEvO2fa8R1jOAwW7K3KS9BL4XIeTj+Uz0pLEPq2HqfgdtT6y3ycz1AHsuhiqnfDaP0gY4+5uhSxJSpH0dfhz1TqrQF9tQtU4EGHs1kvaAB7bTn6OxVA781o92kxE9Crb4IW7zD3nteLzeMX+xgkoFlSDgmcRrpG0XElXHxtFbIw8R2DNFZVYa8KWgtBlDpxsSVn3RaNXGGnxq03zSfUTL+eAgPn9hpboGtuJYC+uH7JjqyRWqJ0zdCnlh314PBwt+ohPj3eyhVyKTfMiBuEsuY7nMEP2u/Buxa8nnyeWRP/i7NsPYIZ+kIqFORdtQWhLrX8qyUEH/8gB667PzdpSMNDDV1jKYnm+Dc3yUC6+cRYMG3yA6D5pQFp1MpUpUpKtCnX0Ao2/PFV5EVPtqqls3wistd2uw/xUbNBPtsByOL+pQ6pvhPNYA/VapsxPrehPll+Ol2xs5bjTgD84W1D2hiS0IUJeysnBi3JUovBhqGI58AKedyiFWdquJCoU/lg/NZSiJ9jhKDSrM8nEq7T1PyFoZc+ahLqW8PdiJQd9fMJAl4cVYWAPjcDgcDidHWd4iDg6Hw+Fw1hguwDgcDoeTl3ABxuFwOJy8hAswDofD4eQlXIBxOBwOJy/hAozD4XA4eQkXYBwOh8PJS7gA43A4HE5ewgUYh8PhcPISLsA4HA6Hk5dwAcbhLAR7QenmzeiZkM+zCHtx6mr9FoezHshIgAWHrNDKXkx5I8txvhMwdtIOy55yyeusthL1hx1xt/aJhKbg6WpCbbVWiru5HMb9rXB/liLumhKE28LSp51X/8Jj7XLd7IFfDuNkTlSIJm7a6lo0MZcwOey/Nvghq+v9vOyXiuiZuh6VWqk9Ve61w/Gfado760uON8W8WGur69E6NJXCp6DMjQD1JxaUs/rTld0SWboAm3aj/Y9uMNcDnBznWz96TFqYWxzwTMjvWxem4HXaUV/hSG7k4QB6nquEpcMF32fRHioI/4f9sFJF7flrLvkMFhD0SFXw1IXEuwjDf8E1300GZ0UQPvPB1WGFcVc9XNfkwBxDuMbqeq75t85NwhM9MGqZZ2ovpsRGI2DqIwfspsdh/2iuWKJB46FdMLe5Yl6shc+86D9AA+K53s0FP1xt9Sh/qIb6E0/M00M2WaIAo5voeBXuQhte+h/c8UCuE3jPjvYJFfQvOjF6Ke559spfBtFWr0xybRCijp/FFb3UXpHjXr2C0YFGaEjUtXuZE8DcYrfRBHj8iKUs7IdvsASNlio5gHO7MF9XsXpzcQQDL+qhErxoesuTfuTNyQsUKjWKDM0YODcplzG193bm402AwzmcJHiEoVbRP53m2U4MXZTqw+RwJ+pKAX9HKxyX5YjMp+AbRjQd92L2URucp9uwGq1xSQIsONSOV8+oYft9A3TZ9WnOWQEkz7Ma/LxGB7XssJGhKNTA9HJdkg+qcPgm/S/AAw+WQBmVbBsUUO94SIxX8l+y5cln+dxTUYFnhLMYkxtP2E8aQvnTqP6v7Owm3ZMYLEGjQneiebTCCMth0kJvyJ8nEcLUSA+azJWyOVKLyt+m89ZLcalx18vXZWYV+8kxCN/JHyeRSdwSKCjLg94e0oCl+OX1rXBfS6FdZHRvy0fxgyLoLTbsLaaTwSlMScEEc6q5GZYhGsZ/F4S3yyqbpMpR30Yj8Hn3l2GesbJINIG3uTGVKD3l+Um2SQ4a22GUz6ObmLZEZNN6NA3p8kwypVrh+So5zWnLIp8oNKCtswH6LdHOnNr7kzbYdtKhV0iwZARx/l89QLENzU0GlMi+ApVbDWh+2UY11Y+z/xEdRiqhIcHVcGwE5/oaobvvLjk8uywuwKbdaD3gRklrBxp/knudGWc+SiXTkj049a43TecQR6X7OepUAbQ+V4/2kQBC1PuHrnnRc+A3cKgM2P9EssvFNUUQcJXtN2igq52RG49kPqx4TIeS+4roPAgh1hkJcLcYYU00j173w+O0w9jQH9fgREIYa6tH5b52uMam5EYsYOqzVIYQ+s0uinugH175usys4mgxY9ehuJNMiUziMu7BpX+phbG+HW45ftDbD+svuzGWbK/J4N5WkGLFPOeE//jyPHpMJLQ6SMCISSFhdtyCX59ITEVmeRbolcsi0QR+nATkyduZU5HNYS2OWBpieVZthXtaCopzDe+zeaKENKcui3VEYvkKl+G7QEOqp/TQJBR6+KsxOE64xDoW8F+LCTylvhHNNUUkylYR5tAyPV9EzjZuimxqPEtHEjPufZFNmzZFuv1yACf3+OZSpK9hh1hOm/T7It3ui5GZWfmzVATPR179pRxf3h5p7Iv4ZuTPc4Uvz0b2yXVv1vdaZEfd+1QvL0a6d/wmMvw1fe7vprTvi5z9UopOtTUy/EZ35Kz/i8jsLTlodiZy/sgeircj0v2JHEaI12P3/eL7kUtfRzNrNnLz/GtifiTW91n6nV0UtufI+cgX30QDZyK+Pz9H19gRec0Xz+xM4kbbFkub+fXzUpnduhnxvb5LDH/tYymexNLvLRNSte/Zr69GhsXrborseuuSHMqgvBfTS9tTv4ucDdyUgm/6Iq/9dwrb0R2Jxs4kH2LX/f1w5GY0+NZs5Av/+5FX30n8/TgX32Dp6KZvpueLf31OTOue35+lMpYDY2nYFNlxxEclLpFYFs/92ReZYXmctizWAX97P/Icy5sTCfkb6BPLbJ9b7ghuXo2cfcUs5pWUN7QllHESclvd9MZCJXL7LKiBBc+0wvqxAZ2kPq6Fg3POMrm7BA195zDypg0GhR/tB4zQbmNmnTkmmCj3FuKBbfcnuYoPBqYQvJG7sx0KTRlMn57HxNAYTpVXQCebN5JRoeqFRhhK1VBskIMUKugfq6ADGjfekoJE7evDHgiqRrS9YkLJD6LDTQWU98w3hQQunEKguBktL+rjJlq6rs6yHya6rmsybmTLJG4UzcFenDioh4olY4MSOn21GD71ZXSsy1jqvS2P9j1xM9y2hyph6fWTtm5DS20KjbzUhkFHCwzF8thbqUMFmwChZEQVlczygbQAZq78xBdfNcvM2qUmNJuXaxEIYsztJQ2D0mCPm8OkNLTApqfk0j3O1VxZWfRadFCxPE5bFvkOaaZHm+Clcmz+RUL+hkkTpl2B4ibGSKMu314J64APYCZE5ygGnqcPE8p4LUgvwK67YLf5YXiZOsFCOYyTRyhRVNmIzuFxTJ4bQLNBgQAzwexugifRVMJWLNaxihlExZERTF4Zh7OpCmoq/6ZcW4UYnsU/5EOSYCgz+vHqH0+J5sO42cKPYGLfIi4XtsSWAIvbnnb5wyg3McNWWD18P4rm2sfmIWD6U/qBy62oiV4vthnRw2L8XSCRmGncOBU7NfPMdClZ0r3dLioU6UywHRvEB6caoUmYU42h180L17zAJvzZQiBGpvlQgrojzdBPO2Ct3g5ttRWtgx4EEss1YwQIF2hXpUmaA5ZQo2QnC72E6a+kkChLLou8JQjPoVpJUTk2p3wVCjGvHPsqYWZzmqoyaY5ruBMNursQZuVBo961zJ+0Akz45Dy8VOjuA/IkqrxpD3jEz6MjtHmTpJycQ7lFj4bOEQyylUYkmH737lh8ZCyuWKR23f4O2oxFULIR6fO9GBpooLpJ2ptrbF4Hu2Z8LcAHEq6iqqiARrcbgkCC7MFEqzvVx6j2Me2GdRdbLuyJLQFOTQjCp/JhvrDke1se8VWI4xhxtqGxRiNpIauEorgBA75JjAy0YfeD09TJWlCj1aKWtKTsDalI81vFe1xzvp2Cy2aEZbQUnac75ysq9xZAClKjqsmJcd87CXNcMwiyNrOzCAXi+dqwpFWInPWB2vA0TLQXrsc1hGt+ZiSow9OPJhuJlfpqPMMOnIGEVWc5wvelnWJnM3WwvTBslM7nEhjpg1uQHxG4Gu2QaTttk2NEKYD6Ydr9bYaaZSJsgch5+TiKEirWqne2YTR6vbnbK3q5kWcSNzOWfm+5wDLzYYMSRXoTmo8MYvTKKHrNBfAdfR1n0wrsGYTSjrZks2Ti4xcxgghcoNDiB1B4pzzmGvKjZ68ZTRd0qYUXY+MWPMTyrLgO+5+XzahRLo/h7GXSlUsKmRK2ZqQVYKqa3pQVbfyYtLo/OkLrrblTSjxfCKDf2g/P5SBCCUPVcCiIseN9YIvCVT+OVjq5YyFN6/xHbAWiGAh8F0bQex5i120uAVvblxfIJo9ZeeWl9DgBCadCNZSs8bH7mnCj58TcpfEqbNHQNy/3oe9MUBrh3wjA3WKGsWPuqjf6DQ0NAy60w97rxdSNhfSBTOJmxtLvLRfIMB++8qCHvfljOhTXtr5fgC0/ZZX1KoQUQkqlKqP/Drw/RPU4zeMJOgMr41bYj3oR/FYODgvwdvwW7V5A85QuhXlxHXJjDO3PGdH+9wr0phNeIpRnT2mkPGvxICgXRvi6B/bDrdTT6FH36NrmGNfA1h1hhN2tsOwqx/ZtcdPvtu3lMFPDFUob0FkbfRhdQY26GRqqig5bTTz+/dtQXs9eyaSBzZQ4v7S2CNOX5KM0yCaP6AR70U/qSDQF0PPM9vh97bGi/ePZeaPGkif2w6AS4LaVYxuL+1ANrCdJN7Xb5j2QqWRzi08C3qP1qHxoWyyPo1via64yiZsJmdxbLpBZPoRxib3545HtUlmwje6v8pAHKN0L/U/kaAmoH9SL822ew1SP749fN3GKo6S2BTb2AG5vPcofkONs06K+ywfo5ixgWMf43zFL+X3dBcsj8byKbQmvfyr5RbOUZyctKJf7h20VFjjYyw+OtcD0QzkikfQasjIrxMmmDmPK664UXICtOzRo8A2i86AJZaVRsyCbiK+izngAo283J6/YK27A4LgTLWY9iqI93w81qDK3wDk+mNfP/in1zXAea4B+q3Rjqq1lMDVRHjhekhcXJLCxCn96uw11einP1Po6tLgG0FKVav2tGoYjH8Bpr0NVLI/TkUncpZPRveUEGeTDRgP+4GxB3RMa+paEupTVXyfGXQ2ptSQ2Z+ai7zxalF6A361B49sj6KW2oZE7XtVW0iLoumkXqNzpyHnW+Xy8fxBXgzo/QGfNytXn5fI9tpZePuZwOBwOJ2/gGhiHw+Fw8hIuwDgcDoeTl3ABxuFwOJy8hAswDofD4eQlXIBxOBwOJy9JuwoxlP6Rdg6Hw+Fw1hjg/wfG7AXuxXC6EQAAAABJRU5ErkJggg==)


```
'''
import pandas as pd

student_data1 = pd.DataFrame({
        'student_id': ['S1', 'S2', 'S3', 'S4', 'S5'],
         'name': ['Danniella Fenton', 'Ryder Storey', 'Bryce Jensen', 'Ed Bernal', 'Kwame Morin'], 
        'marks': [200, 210, 190, 222, 199]})

student_data2 = pd.DataFrame({
        'student_id': ['S4', 'S5', 'S6', 'S7', 'S8'],
        'name': ['Scarlette Fisher', 'Carla Williamson', 'Dante Morse', 'Kaiser William', 'Madeeha Preston'], 
        'marks': [201, 200, 198, 219, 201]})

result_data = pd.concat([student_data1, student_data2])
print(result_data)

'''
```

### 2.0.3 Exercise

Use the same dataframes created in the previous exercise and this time join them along the column


```
'''
result_data = pd.concat([student_data1, student_data2], axis = 1)
print(result_data)
'''
```

### 2.0.4 Exercise

Use the same dataframes created in exercise 2.0.2 and write a Pandas program to join the two dataframes using the common column of both dataframes.


```
'''
merged_data = pd.merge(student_data1, student_data2, on='student_id', how='inner')
print("Merged data (inner join):")
print(merged_data)
'''

```

### 2.0.5 Exercise

Use this dataset for this exercise:

![image.png](data:image/png;base64,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)

Write a Pandas program to join (left join) the two dataframes using keys from left dataframe only.


```
'''
import pandas as pd
data1 = pd.DataFrame({'key1': ['K0', 'K0', 'K1', 'K2'],
                     'key2': ['K0', 'K1', 'K0', 'K1'],
                     'P': ['P0', 'P1', 'P2', 'P3'],
                     'Q': ['Q0', 'Q1', 'Q2', 'Q3']}) 
data2 = pd.DataFrame({'key1': ['K0', 'K1', 'K1', 'K2'],
                      'key2': ['K0', 'K0', 'K0', 'K0'],
                      'R': ['R0', 'R1', 'R2', 'R3'],
                      'S': ['S0', 'S1', 'S2', 'S3']})
print("\nMerged Data (keys from data1):")
merged_data = pd.merge(data1, data2, how='left', on=['key1', 'key2'])
print(merged_data)
print("\nMerged Data (keys from data2):")
merged_data = pd.merge(data2, data1, how='left', on=['key1', 'key2'])
print(merged_data)
'''
```

# 2.1 Merging

Lets consider a case where we have two subjects and for each subject we have two datasets


```
df1SE =  pd.DataFrame({'StudentID': [9, 11, 13, 15, 17, 19, 21, 23, 25, 27, 29], 'ScoreSE' : [22, 66, 31, 51, 71, 91, 56, 32, 52, 73, 92]})
df2SE =  pd.DataFrame({'StudentID': [2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30], 'ScoreSE': [98, 93, 44, 77, 69, 56, 31, 53, 78, 93, 56, 77, 33, 56, 27]})

df1ML =  pd.DataFrame({'StudentID': [1, 3, 5, 7, 9, 11, 13, 15, 17, 19, 21, 23, 25, 27, 29], 'ScoreML' : [39, 49, 55, 77, 52, 86, 41, 77, 73, 51, 86, 82, 92, 23, 49]})
df2ML =  pd.DataFrame({'StudentID': [2, 4, 6, 8, 10, 12, 14, 16, 18, 20], 'ScoreML': [93, 44, 78, 97, 87, 89, 39, 43, 88, 78]})
```

## 2.1.2 Exercise
As you can see in the dataset above, you have two dataframes for each subjects. 

We need to concatenate SE & ML into one dataframe
There are multiple ways to complete the task, Let's go over some ways of doing it. 

##Q1 Concatinate df1SE & df2SE, df1ML & df2ML and then concatenate resulting dataframes together


```
# Option 1 - Try Concatenating df1SE & df2SE, df1ML & df2ML and then concatenate resulting dataframes together,
# no need to match student IDs across subjects


"""
Solution
dfSE = pd.concat([df1SE, df2SE], ignore_index=True)
dfML = pd.concat([df1ML, df2ML], ignore_index=True)

df = pd.concat([dfML, dfSE], axis=1)
"""
```





  <div id="df-6c4ee23a-62b0-43ac-ad67-353c96593bd0">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>StudentID</th>
      <th>ScoreML</th>
      <th>StudentID</th>
      <th>ScoreSE</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>39.0</td>
      <td>9</td>
      <td>22</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3.0</td>
      <td>49.0</td>
      <td>11</td>
      <td>66</td>
    </tr>
    <tr>
      <th>2</th>
      <td>5.0</td>
      <td>55.0</td>
      <td>13</td>
      <td>31</td>
    </tr>
    <tr>
      <th>3</th>
      <td>7.0</td>
      <td>77.0</td>
      <td>15</td>
      <td>51</td>
    </tr>
    <tr>
      <th>4</th>
      <td>9.0</td>
      <td>52.0</td>
      <td>17</td>
      <td>71</td>
    </tr>
    <tr>
      <th>5</th>
      <td>11.0</td>
      <td>86.0</td>
      <td>19</td>
      <td>91</td>
    </tr>
    <tr>
      <th>6</th>
      <td>13.0</td>
      <td>41.0</td>
      <td>21</td>
      <td>56</td>
    </tr>
    <tr>
      <th>7</th>
      <td>15.0</td>
      <td>77.0</td>
      <td>23</td>
      <td>32</td>
    </tr>
    <tr>
      <th>8</th>
      <td>17.0</td>
      <td>73.0</td>
      <td>25</td>
      <td>52</td>
    </tr>
    <tr>
      <th>9</th>
      <td>19.0</td>
      <td>51.0</td>
      <td>27</td>
      <td>73</td>
    </tr>
    <tr>
      <th>10</th>
      <td>21.0</td>
      <td>86.0</td>
      <td>29</td>
      <td>92</td>
    </tr>
    <tr>
      <th>11</th>
      <td>23.0</td>
      <td>82.0</td>
      <td>2</td>
      <td>98</td>
    </tr>
    <tr>
      <th>12</th>
      <td>25.0</td>
      <td>92.0</td>
      <td>4</td>
      <td>93</td>
    </tr>
    <tr>
      <th>13</th>
      <td>27.0</td>
      <td>23.0</td>
      <td>6</td>
      <td>44</td>
    </tr>
    <tr>
      <th>14</th>
      <td>29.0</td>
      <td>49.0</td>
      <td>8</td>
      <td>77</td>
    </tr>
    <tr>
      <th>15</th>
      <td>2.0</td>
      <td>93.0</td>
      <td>10</td>
      <td>69</td>
    </tr>
    <tr>
      <th>16</th>
      <td>4.0</td>
      <td>44.0</td>
      <td>12</td>
      <td>56</td>
    </tr>
    <tr>
      <th>17</th>
      <td>6.0</td>
      <td>78.0</td>
      <td>14</td>
      <td>31</td>
    </tr>
    <tr>
      <th>18</th>
      <td>8.0</td>
      <td>97.0</td>
      <td>16</td>
      <td>53</td>
    </tr>
    <tr>
      <th>19</th>
      <td>10.0</td>
      <td>87.0</td>
      <td>18</td>
      <td>78</td>
    </tr>
    <tr>
      <th>20</th>
      <td>12.0</td>
      <td>89.0</td>
      <td>20</td>
      <td>93</td>
    </tr>
    <tr>
      <th>21</th>
      <td>14.0</td>
      <td>39.0</td>
      <td>22</td>
      <td>56</td>
    </tr>
    <tr>
      <th>22</th>
      <td>16.0</td>
      <td>43.0</td>
      <td>24</td>
      <td>77</td>
    </tr>
    <tr>
      <th>23</th>
      <td>18.0</td>
      <td>88.0</td>
      <td>26</td>
      <td>33</td>
    </tr>
    <tr>
      <th>24</th>
      <td>20.0</td>
      <td>78.0</td>
      <td>28</td>
      <td>56</td>
    </tr>
    <tr>
      <th>25</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>30</td>
      <td>27</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-6c4ee23a-62b0-43ac-ad67-353c96593bd0')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-6c4ee23a-62b0-43ac-ad67-353c96593bd0 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-6c4ee23a-62b0-43ac-ad67-353c96593bd0');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




## Q2 Perform inner join with each dataframe. 
That is to say, if an item exists on the both dataframe, will be included in the new dataframe.
This means, we will get the list of students who are appearing in both the courses.


```
# Option 2
"""
Here, you will perform inner join with each dataframe. 
That is to say, if an item exists on the both dataframe, will be included in the new dataframe.
This means, we will get the list of students who are appearing in both the courses.

Hint: Apply Inner Join using merge()
""" 

"""
Solution
dfSE = pd.concat([df1SE, df2SE], ignore_index=True)
dfML = pd.concat([df1ML, df2ML], ignore_index=True)
df = dfSE.merge(dfML, how='inner')
"""


```





  <div id="df-b6d68b8d-51a2-47e2-9ecb-16ce2e4dac21">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>StudentID</th>
      <th>ScoreSE</th>
      <th>ScoreML</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>9</td>
      <td>22</td>
      <td>52</td>
    </tr>
    <tr>
      <th>1</th>
      <td>11</td>
      <td>66</td>
      <td>86</td>
    </tr>
    <tr>
      <th>2</th>
      <td>13</td>
      <td>31</td>
      <td>41</td>
    </tr>
    <tr>
      <th>3</th>
      <td>15</td>
      <td>51</td>
      <td>77</td>
    </tr>
    <tr>
      <th>4</th>
      <td>17</td>
      <td>71</td>
      <td>73</td>
    </tr>
    <tr>
      <th>5</th>
      <td>19</td>
      <td>91</td>
      <td>51</td>
    </tr>
    <tr>
      <th>6</th>
      <td>21</td>
      <td>56</td>
      <td>86</td>
    </tr>
    <tr>
      <th>7</th>
      <td>23</td>
      <td>32</td>
      <td>82</td>
    </tr>
    <tr>
      <th>8</th>
      <td>25</td>
      <td>52</td>
      <td>92</td>
    </tr>
    <tr>
      <th>9</th>
      <td>27</td>
      <td>73</td>
      <td>23</td>
    </tr>
    <tr>
      <th>10</th>
      <td>29</td>
      <td>92</td>
      <td>49</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2</td>
      <td>98</td>
      <td>93</td>
    </tr>
    <tr>
      <th>12</th>
      <td>4</td>
      <td>93</td>
      <td>44</td>
    </tr>
    <tr>
      <th>13</th>
      <td>6</td>
      <td>44</td>
      <td>78</td>
    </tr>
    <tr>
      <th>14</th>
      <td>8</td>
      <td>77</td>
      <td>97</td>
    </tr>
    <tr>
      <th>15</th>
      <td>10</td>
      <td>69</td>
      <td>87</td>
    </tr>
    <tr>
      <th>16</th>
      <td>12</td>
      <td>56</td>
      <td>89</td>
    </tr>
    <tr>
      <th>17</th>
      <td>14</td>
      <td>31</td>
      <td>39</td>
    </tr>
    <tr>
      <th>18</th>
      <td>16</td>
      <td>53</td>
      <td>43</td>
    </tr>
    <tr>
      <th>19</th>
      <td>18</td>
      <td>78</td>
      <td>88</td>
    </tr>
    <tr>
      <th>20</th>
      <td>20</td>
      <td>93</td>
      <td>78</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-b6d68b8d-51a2-47e2-9ecb-16ce2e4dac21')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-b6d68b8d-51a2-47e2-9ecb-16ce2e4dac21 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-b6d68b8d-51a2-47e2-9ecb-16ce2e4dac21');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




##Q3 Performing Left Join on Dataframes



```
# Option 3
"""
Here, you will perform left join with each dataframe. 
That is to say, if an item exists either in first dataframe or on the both dataframe, will be included in the new dataframe.

Hint: Apply Left Join using merge()
""" 

"""
Solution
dfSE = pd.concat([df1SE, df2SE], ignore_index=True)
dfML = pd.concat([df1ML, df2ML], ignore_index=True)

df = dfSE.merge(dfML, how='left')
"""
```





  <div id="df-279da236-0ffd-497d-88e2-6c79fe8ee5db">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>StudentID</th>
      <th>ScoreSE</th>
      <th>ScoreML</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>9</td>
      <td>22</td>
      <td>52.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>11</td>
      <td>66</td>
      <td>86.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>13</td>
      <td>31</td>
      <td>41.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>15</td>
      <td>51</td>
      <td>77.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>17</td>
      <td>71</td>
      <td>73.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>19</td>
      <td>91</td>
      <td>51.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>21</td>
      <td>56</td>
      <td>86.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>23</td>
      <td>32</td>
      <td>82.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>25</td>
      <td>52</td>
      <td>92.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>27</td>
      <td>73</td>
      <td>23.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>29</td>
      <td>92</td>
      <td>49.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2</td>
      <td>98</td>
      <td>93.0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>4</td>
      <td>93</td>
      <td>44.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>6</td>
      <td>44</td>
      <td>78.0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>8</td>
      <td>77</td>
      <td>97.0</td>
    </tr>
    <tr>
      <th>15</th>
      <td>10</td>
      <td>69</td>
      <td>87.0</td>
    </tr>
    <tr>
      <th>16</th>
      <td>12</td>
      <td>56</td>
      <td>89.0</td>
    </tr>
    <tr>
      <th>17</th>
      <td>14</td>
      <td>31</td>
      <td>39.0</td>
    </tr>
    <tr>
      <th>18</th>
      <td>16</td>
      <td>53</td>
      <td>43.0</td>
    </tr>
    <tr>
      <th>19</th>
      <td>18</td>
      <td>78</td>
      <td>88.0</td>
    </tr>
    <tr>
      <th>20</th>
      <td>20</td>
      <td>93</td>
      <td>78.0</td>
    </tr>
    <tr>
      <th>21</th>
      <td>22</td>
      <td>56</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>22</th>
      <td>24</td>
      <td>77</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>23</th>
      <td>26</td>
      <td>33</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>24</th>
      <td>28</td>
      <td>56</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>25</th>
      <td>30</td>
      <td>27</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-279da236-0ffd-497d-88e2-6c79fe8ee5db')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-279da236-0ffd-497d-88e2-6c79fe8ee5db button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-279da236-0ffd-497d-88e2-6c79fe8ee5db');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




##Q4 Performing Right join on Dataframes


```
# Option 4
"""
Here, you will perform Right join with each dataframe. 
That is to say, if an item exists either in second dataframe or on the both dataframe, will be included in the new dataframe.

Hint: Apply Right Join using merge()
""" 

"""
Solution
dfSE = pd.concat([df1SE, df2SE], ignore_index=True)
dfML = pd.concat([df1ML, df2ML], ignore_index=True)

df = dfSE.merge(dfML, how='right')
"""
```





  <div id="df-ad5067ec-af98-47d0-a93e-8f23e5a84b01">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>StudentID</th>
      <th>ScoreSE</th>
      <th>ScoreML</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>NaN</td>
      <td>39</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3</td>
      <td>NaN</td>
      <td>49</td>
    </tr>
    <tr>
      <th>2</th>
      <td>5</td>
      <td>NaN</td>
      <td>55</td>
    </tr>
    <tr>
      <th>3</th>
      <td>7</td>
      <td>NaN</td>
      <td>77</td>
    </tr>
    <tr>
      <th>4</th>
      <td>9</td>
      <td>22.0</td>
      <td>52</td>
    </tr>
    <tr>
      <th>5</th>
      <td>11</td>
      <td>66.0</td>
      <td>86</td>
    </tr>
    <tr>
      <th>6</th>
      <td>13</td>
      <td>31.0</td>
      <td>41</td>
    </tr>
    <tr>
      <th>7</th>
      <td>15</td>
      <td>51.0</td>
      <td>77</td>
    </tr>
    <tr>
      <th>8</th>
      <td>17</td>
      <td>71.0</td>
      <td>73</td>
    </tr>
    <tr>
      <th>9</th>
      <td>19</td>
      <td>91.0</td>
      <td>51</td>
    </tr>
    <tr>
      <th>10</th>
      <td>21</td>
      <td>56.0</td>
      <td>86</td>
    </tr>
    <tr>
      <th>11</th>
      <td>23</td>
      <td>32.0</td>
      <td>82</td>
    </tr>
    <tr>
      <th>12</th>
      <td>25</td>
      <td>52.0</td>
      <td>92</td>
    </tr>
    <tr>
      <th>13</th>
      <td>27</td>
      <td>73.0</td>
      <td>23</td>
    </tr>
    <tr>
      <th>14</th>
      <td>29</td>
      <td>92.0</td>
      <td>49</td>
    </tr>
    <tr>
      <th>15</th>
      <td>2</td>
      <td>98.0</td>
      <td>93</td>
    </tr>
    <tr>
      <th>16</th>
      <td>4</td>
      <td>93.0</td>
      <td>44</td>
    </tr>
    <tr>
      <th>17</th>
      <td>6</td>
      <td>44.0</td>
      <td>78</td>
    </tr>
    <tr>
      <th>18</th>
      <td>8</td>
      <td>77.0</td>
      <td>97</td>
    </tr>
    <tr>
      <th>19</th>
      <td>10</td>
      <td>69.0</td>
      <td>87</td>
    </tr>
    <tr>
      <th>20</th>
      <td>12</td>
      <td>56.0</td>
      <td>89</td>
    </tr>
    <tr>
      <th>21</th>
      <td>14</td>
      <td>31.0</td>
      <td>39</td>
    </tr>
    <tr>
      <th>22</th>
      <td>16</td>
      <td>53.0</td>
      <td>43</td>
    </tr>
    <tr>
      <th>23</th>
      <td>18</td>
      <td>78.0</td>
      <td>88</td>
    </tr>
    <tr>
      <th>24</th>
      <td>20</td>
      <td>93.0</td>
      <td>78</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-ad5067ec-af98-47d0-a93e-8f23e5a84b01')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-ad5067ec-af98-47d0-a93e-8f23e5a84b01 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-ad5067ec-af98-47d0-a93e-8f23e5a84b01');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




##Q5 Performing Outer Join on Dataframes


```
# Option 5
"""
Here, you will perform outer join with each dataframe. 
That is to say, if an item exists in either of the dataframes, will be included in the new dataframe.

Hint: Apply Outer Join using merge()
""" 

"""
Solution
dfSE = pd.concat([df1SE, df2SE], ignore_index=True)
dfML = pd.concat([df1ML, df2ML], ignore_index=True)

df = dfSE.merge(dfML, how='outer')
"""
```





  <div id="df-85a4c6f9-91fc-494e-8ccd-0d8e16a4f74b">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>StudentID</th>
      <th>ScoreSE</th>
      <th>ScoreML</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>9</td>
      <td>22.0</td>
      <td>52.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>11</td>
      <td>66.0</td>
      <td>86.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>13</td>
      <td>31.0</td>
      <td>41.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>15</td>
      <td>51.0</td>
      <td>77.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>17</td>
      <td>71.0</td>
      <td>73.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>19</td>
      <td>91.0</td>
      <td>51.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>21</td>
      <td>56.0</td>
      <td>86.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>23</td>
      <td>32.0</td>
      <td>82.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>25</td>
      <td>52.0</td>
      <td>92.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>27</td>
      <td>73.0</td>
      <td>23.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>29</td>
      <td>92.0</td>
      <td>49.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2</td>
      <td>98.0</td>
      <td>93.0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>4</td>
      <td>93.0</td>
      <td>44.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>6</td>
      <td>44.0</td>
      <td>78.0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>8</td>
      <td>77.0</td>
      <td>97.0</td>
    </tr>
    <tr>
      <th>15</th>
      <td>10</td>
      <td>69.0</td>
      <td>87.0</td>
    </tr>
    <tr>
      <th>16</th>
      <td>12</td>
      <td>56.0</td>
      <td>89.0</td>
    </tr>
    <tr>
      <th>17</th>
      <td>14</td>
      <td>31.0</td>
      <td>39.0</td>
    </tr>
    <tr>
      <th>18</th>
      <td>16</td>
      <td>53.0</td>
      <td>43.0</td>
    </tr>
    <tr>
      <th>19</th>
      <td>18</td>
      <td>78.0</td>
      <td>88.0</td>
    </tr>
    <tr>
      <th>20</th>
      <td>20</td>
      <td>93.0</td>
      <td>78.0</td>
    </tr>
    <tr>
      <th>21</th>
      <td>22</td>
      <td>56.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>22</th>
      <td>24</td>
      <td>77.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>23</th>
      <td>26</td>
      <td>33.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>24</th>
      <td>28</td>
      <td>56.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>25</th>
      <td>30</td>
      <td>27.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>26</th>
      <td>1</td>
      <td>NaN</td>
      <td>39.0</td>
    </tr>
    <tr>
      <th>27</th>
      <td>3</td>
      <td>NaN</td>
      <td>49.0</td>
    </tr>
    <tr>
      <th>28</th>
      <td>5</td>
      <td>NaN</td>
      <td>55.0</td>
    </tr>
    <tr>
      <th>29</th>
      <td>7</td>
      <td>NaN</td>
      <td>77.0</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-85a4c6f9-91fc-494e-8ccd-0d8e16a4f74b')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-85a4c6f9-91fc-494e-8ccd-0d8e16a4f74b button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-85a4c6f9-91fc-494e-8ccd-0d8e16a4f74b');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```
df = pd.read_csv("https://drive.google.com/uc?id=1fh7UdeQO0p_yWUAKcCinv9dElxaWQ5Ya")
df.head(10)
```





  <div id="df-e7708650-2e31-449b-9cc8-a6ee12fd7931">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>Account</th>
      <th>Company</th>
      <th>Order</th>
      <th>SKU</th>
      <th>Country</th>
      <th>Year</th>
      <th>Quantity</th>
      <th>UnitPrice</th>
      <th>transactionComplete</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>123456779</td>
      <td>Kulas Inc</td>
      <td>99985</td>
      <td>s9-supercomputer</td>
      <td>Aruba</td>
      <td>1981</td>
      <td>5148</td>
      <td>545</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>123456784</td>
      <td>GitHub</td>
      <td>99986</td>
      <td>s4-supercomputer</td>
      <td>Brazil</td>
      <td>2001</td>
      <td>3262</td>
      <td>383</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>123456782</td>
      <td>Kulas Inc</td>
      <td>99990</td>
      <td>s10-supercomputer</td>
      <td>Montserrat</td>
      <td>1973</td>
      <td>9119</td>
      <td>407</td>
      <td>True</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>123456783</td>
      <td>My SQ Man</td>
      <td>99999</td>
      <td>s1-supercomputer</td>
      <td>El Salvador</td>
      <td>2015</td>
      <td>3097</td>
      <td>615</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>123456787</td>
      <td>ABC Dogma</td>
      <td>99996</td>
      <td>s6-supercomputer</td>
      <td>Poland</td>
      <td>1970</td>
      <td>3356</td>
      <td>91</td>
      <td>True</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>123456778</td>
      <td>Super Sexy Dingo</td>
      <td>99996</td>
      <td>s9-supercomputer</td>
      <td>Costa Rica</td>
      <td>2004</td>
      <td>2474</td>
      <td>136</td>
      <td>True</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>123456783</td>
      <td>ABC Dogma</td>
      <td>99981</td>
      <td>s11-supercomputer</td>
      <td>Spain</td>
      <td>2006</td>
      <td>4081</td>
      <td>195</td>
      <td>False</td>
    </tr>
    <tr>
      <th>7</th>
      <td>7</td>
      <td>123456785</td>
      <td>ABC Dogma</td>
      <td>99998</td>
      <td>s9-supercomputer</td>
      <td>Belarus</td>
      <td>2015</td>
      <td>6576</td>
      <td>603</td>
      <td>False</td>
    </tr>
    <tr>
      <th>8</th>
      <td>8</td>
      <td>123456778</td>
      <td>Loolo INC</td>
      <td>99997</td>
      <td>s8-supercomputer</td>
      <td>Mauritius</td>
      <td>1999</td>
      <td>2460</td>
      <td>36</td>
      <td>False</td>
    </tr>
    <tr>
      <th>9</th>
      <td>9</td>
      <td>123456775</td>
      <td>Kulas Inc</td>
      <td>99997</td>
      <td>s7-supercomputer</td>
      <td>French Guiana</td>
      <td>2004</td>
      <td>1831</td>
      <td>664</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-e7708650-2e31-449b-9cc8-a6ee12fd7931')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-e7708650-2e31-449b-9cc8-a6ee12fd7931 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-e7708650-2e31-449b-9cc8-a6ee12fd7931');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```
#Task: Add new colum that is the total price based on the product of quantity and the unit price

"""
Solution
df['TotalPrice'] = df['UnitPrice'] * df['Quantity']
df.head(10)
"""
```





  <div id="df-3d6e0cd2-b1a2-4efd-a699-8b57ab4dc234">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Account</th>
      <th>Company</th>
      <th>Order</th>
      <th>SKU</th>
      <th>Country</th>
      <th>Year</th>
      <th>Quantity</th>
      <th>UnitPrice</th>
      <th>transactionComplete</th>
      <th>TotalPrice</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>123456779</td>
      <td>Kulas Inc</td>
      <td>99985</td>
      <td>s9-supercomputer</td>
      <td>Aruba</td>
      <td>1981</td>
      <td>5148</td>
      <td>545</td>
      <td>False</td>
      <td>2805660</td>
    </tr>
    <tr>
      <th>1</th>
      <td>123456784</td>
      <td>GitHub</td>
      <td>99986</td>
      <td>s4-supercomputer</td>
      <td>Brazil</td>
      <td>2001</td>
      <td>3262</td>
      <td>383</td>
      <td>False</td>
      <td>1249346</td>
    </tr>
    <tr>
      <th>2</th>
      <td>123456782</td>
      <td>Kulas Inc</td>
      <td>99990</td>
      <td>s10-supercomputer</td>
      <td>Montserrat</td>
      <td>1973</td>
      <td>9119</td>
      <td>407</td>
      <td>True</td>
      <td>3711433</td>
    </tr>
    <tr>
      <th>3</th>
      <td>123456783</td>
      <td>My SQ Man</td>
      <td>99999</td>
      <td>s1-supercomputer</td>
      <td>El Salvador</td>
      <td>2015</td>
      <td>3097</td>
      <td>615</td>
      <td>False</td>
      <td>1904655</td>
    </tr>
    <tr>
      <th>4</th>
      <td>123456787</td>
      <td>ABC Dogma</td>
      <td>99996</td>
      <td>s6-supercomputer</td>
      <td>Poland</td>
      <td>1970</td>
      <td>3356</td>
      <td>91</td>
      <td>True</td>
      <td>305396</td>
    </tr>
    <tr>
      <th>5</th>
      <td>123456778</td>
      <td>Super Sexy Dingo</td>
      <td>99996</td>
      <td>s9-supercomputer</td>
      <td>Costa Rica</td>
      <td>2004</td>
      <td>2474</td>
      <td>136</td>
      <td>True</td>
      <td>336464</td>
    </tr>
    <tr>
      <th>6</th>
      <td>123456783</td>
      <td>ABC Dogma</td>
      <td>99981</td>
      <td>s11-supercomputer</td>
      <td>Spain</td>
      <td>2006</td>
      <td>4081</td>
      <td>195</td>
      <td>False</td>
      <td>795795</td>
    </tr>
    <tr>
      <th>7</th>
      <td>123456785</td>
      <td>ABC Dogma</td>
      <td>99998</td>
      <td>s9-supercomputer</td>
      <td>Belarus</td>
      <td>2015</td>
      <td>6576</td>
      <td>603</td>
      <td>False</td>
      <td>3965328</td>
    </tr>
    <tr>
      <th>8</th>
      <td>123456778</td>
      <td>Loolo INC</td>
      <td>99997</td>
      <td>s8-supercomputer</td>
      <td>Mauritius</td>
      <td>1999</td>
      <td>2460</td>
      <td>36</td>
      <td>False</td>
      <td>88560</td>
    </tr>
    <tr>
      <th>9</th>
      <td>123456775</td>
      <td>Kulas Inc</td>
      <td>99997</td>
      <td>s7-supercomputer</td>
      <td>French Guiana</td>
      <td>2004</td>
      <td>1831</td>
      <td>664</td>
      <td>True</td>
      <td>1215784</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-3d6e0cd2-b1a2-4efd-a699-8b57ab4dc234')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-3d6e0cd2-b1a2-4efd-a699-8b57ab4dc234 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-3d6e0cd2-b1a2-4efd-a699-8b57ab4dc234');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```
df['Company'].value_counts()
```




    My SQ Man                   869
    Kirlosker Service Center    863
    Will LLC                    862
    ABC Dogma                   848
    Kulas Inc                   840
    Gen Power                   836
    Name IT                     836
    Super Sexy Dingo            828
    GitHub                      823
    Loolo INC                   822
    SAS Web Tec                 798
    Pryianka Ji                 775
    Name: Company, dtype: int64




```
df.describe()
```





  <div id="df-722a411f-dc21-4bec-b930-aa7aa1f44954">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Account</th>
      <th>Order</th>
      <th>Year</th>
      <th>Quantity</th>
      <th>UnitPrice</th>
      <th>TotalPrice</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>1.000000e+04</td>
      <td>10000.000000</td>
      <td>10000.000000</td>
      <td>10000.000000</td>
      <td>10000.000000</td>
      <td>1.000000e+04</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>1.234568e+08</td>
      <td>99989.562900</td>
      <td>1994.619800</td>
      <td>4985.447300</td>
      <td>355.866600</td>
      <td>1.773301e+06</td>
    </tr>
    <tr>
      <th>std</th>
      <td>5.741156e+00</td>
      <td>5.905551</td>
      <td>14.432771</td>
      <td>2868.949686</td>
      <td>201.378478</td>
      <td>1.540646e+06</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.234568e+08</td>
      <td>99980.000000</td>
      <td>1970.000000</td>
      <td>0.000000</td>
      <td>10.000000</td>
      <td>0.000000e+00</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>1.234568e+08</td>
      <td>99985.000000</td>
      <td>1982.000000</td>
      <td>2505.750000</td>
      <td>181.000000</td>
      <td>5.003370e+05</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>1.234568e+08</td>
      <td>99990.000000</td>
      <td>1995.000000</td>
      <td>4994.000000</td>
      <td>356.000000</td>
      <td>1.335698e+06</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>1.234568e+08</td>
      <td>99995.000000</td>
      <td>2007.000000</td>
      <td>7451.500000</td>
      <td>531.000000</td>
      <td>2.711653e+06</td>
    </tr>
    <tr>
      <th>max</th>
      <td>1.234568e+08</td>
      <td>99999.000000</td>
      <td>2019.000000</td>
      <td>9999.000000</td>
      <td>700.000000</td>
      <td>6.841580e+06</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-722a411f-dc21-4bec-b930-aa7aa1f44954')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-722a411f-dc21-4bec-b930-aa7aa1f44954 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-722a411f-dc21-4bec-b930-aa7aa1f44954');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




##Q6 Merging with Hierarchical Indexing


```
data = np.arange(15).reshape((3,5))
indexers = ['Rainfall', 'Humidity', 'Wind']
dframe1 = pd.DataFrame(data, index=indexers, columns=['Lucknow', 'Delhi', 'Bengaluru', 'Chennai', 'Kolkata'])
dframe1
```





  <div id="df-0c073858-adb7-4eb9-ac26-2426b41f3096">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Lucknow</th>
      <th>Delhi</th>
      <th>Bengaluru</th>
      <th>Chennai</th>
      <th>Kolkata</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Rainfall</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>Humidity</th>
      <td>5</td>
      <td>6</td>
      <td>7</td>
      <td>8</td>
      <td>9</td>
    </tr>
    <tr>
      <th>Wind</th>
      <td>10</td>
      <td>11</td>
      <td>12</td>
      <td>13</td>
      <td>14</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-0c073858-adb7-4eb9-ac26-2426b41f3096')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-0c073858-adb7-4eb9-ac26-2426b41f3096 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-0c073858-adb7-4eb9-ac26-2426b41f3096');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```
stacked = dframe1.stack()
stacked
```




    Rainfall  Lucknow       0
              Delhi         1
              Bengaluru     2
              Chennai       3
              Kolkata       4
    Humidity  Lucknow       5
              Delhi         6
              Bengaluru     7
              Chennai       8
              Kolkata       9
    Wind      Lucknow      10
              Delhi        11
              Bengaluru    12
              Chennai      13
              Kolkata      14
    dtype: int64




```
stacked.unstack()
```





  <div id="df-65f88e44-7183-47fc-9bd5-988aeddcb671">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Lucknow</th>
      <th>Delhi</th>
      <th>Bengaluru</th>
      <th>Chennai</th>
      <th>Kolkata</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Rainfall</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>Humidity</th>
      <td>5</td>
      <td>6</td>
      <td>7</td>
      <td>8</td>
      <td>9</td>
    </tr>
    <tr>
      <th>Wind</th>
      <td>10</td>
      <td>11</td>
      <td>12</td>
      <td>13</td>
      <td>14</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-65f88e44-7183-47fc-9bd5-988aeddcb671')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-65f88e44-7183-47fc-9bd5-988aeddcb671 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-65f88e44-7183-47fc-9bd5-988aeddcb671');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```
series1 = pd.Series([000, 111, 222, 333], index=['zeros','ones', 'twos', 'threes'])
series2 = pd.Series([444, 555, 666], index=['fours', 'fives', 'sixs'])

frame2 = pd.concat([series1, series2], keys=['Number1', 'Number2'])
print(frame2)

"""
How would frame2 look if we try to unstack it?
Try to use unstack() on frame2 
"""

"""
Solution
frame2.unstack()
"""
```

    Number1  zeros       0
             ones      111
             twos      222
             threes    333
    Number2  fours     444
             fives     555
             sixs      666
    dtype: int64






  <div id="df-a4900e5d-f554-4c9f-ae4c-0af16d545f0d">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>fives</th>
      <th>fours</th>
      <th>ones</th>
      <th>sixs</th>
      <th>threes</th>
      <th>twos</th>
      <th>zeros</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Number1</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>111.0</td>
      <td>NaN</td>
      <td>333.0</td>
      <td>222.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>Number2</th>
      <td>555.0</td>
      <td>444.0</td>
      <td>NaN</td>
      <td>666.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-a4900e5d-f554-4c9f-ae4c-0af16d545f0d')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-a4900e5d-f554-4c9f-ae4c-0af16d545f0d button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-a4900e5d-f554-4c9f-ae4c-0af16d545f0d');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```

```


```

```


```

```


```

```

# 2.2 Data deduplication


```
frame3 = pd.DataFrame({'column 1': ['Looping'] * 3 + ['Functions'] * 4, 'column 2': [10, 10, 22, 23, 23, 24, 24]})
frame3
```





  <div id="df-eef2af0d-0342-4899-8a60-5c3b50cd82e0">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>column 1</th>
      <th>column 2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Looping</td>
      <td>10</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Looping</td>
      <td>10</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Looping</td>
      <td>22</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Functions</td>
      <td>23</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Functions</td>
      <td>23</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Functions</td>
      <td>24</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Functions</td>
      <td>24</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-eef2af0d-0342-4899-8a60-5c3b50cd82e0')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-eef2af0d-0342-4899-8a60-5c3b50cd82e0 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-eef2af0d-0342-4899-8a60-5c3b50cd82e0');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




## 2.2.1 Exercise


```
"""
Exercise: Check for duplicates in frame3 without dropping them.
"""

"""
Solution
frame3.duplicated()
"""
```




    '\nSolution\nframe3.duplicated()\n'




```
import pandas as pd
help(pd.DataFrame.drop_duplicates)
```

    Help on function drop_duplicates in module pandas.core.frame:
    
    drop_duplicates(self, subset: 'Hashable | Sequence[Hashable] | None' = None, keep: "Literal['first'] | Literal['last'] | Literal[False]" = 'first', inplace: 'bool' = False, ignore_index: 'bool' = False) -> 'DataFrame | None'
        Return DataFrame with duplicate rows removed.
        
        Considering certain columns is optional. Indexes, including time indexes
        are ignored.
        
        Parameters
        ----------
        subset : column label or sequence of labels, optional
            Only consider certain columns for identifying duplicates, by
            default use all of the columns.
        keep : {'first', 'last', False}, default 'first'
            Determines which duplicates (if any) to keep.
            - ``first`` : Drop duplicates except for the first occurrence.
            - ``last`` : Drop duplicates except for the last occurrence.
            - False : Drop all duplicates.
        inplace : bool, default False
            Whether to drop duplicates in place or to return a copy.
        ignore_index : bool, default False
            If True, the resulting axis will be labeled 0, 1, …, n - 1.
        
            .. versionadded:: 1.0.0
        
        Returns
        -------
        DataFrame or None
            DataFrame with duplicates removed or None if ``inplace=True``.
        
        See Also
        --------
        DataFrame.value_counts: Count unique combinations of columns.
        
        Examples
        --------
        Consider dataset containing ramen rating.
        
        >>> df = pd.DataFrame({
        ...     'brand': ['Yum Yum', 'Yum Yum', 'Indomie', 'Indomie', 'Indomie'],
        ...     'style': ['cup', 'cup', 'cup', 'pack', 'pack'],
        ...     'rating': [4, 4, 3.5, 15, 5]
        ... })
        >>> df
            brand style  rating
        0  Yum Yum   cup     4.0
        1  Yum Yum   cup     4.0
        2  Indomie   cup     3.5
        3  Indomie  pack    15.0
        4  Indomie  pack     5.0
        
        By default, it removes duplicate rows based on all columns.
        
        >>> df.drop_duplicates()
            brand style  rating
        0  Yum Yum   cup     4.0
        2  Indomie   cup     3.5
        3  Indomie  pack    15.0
        4  Indomie  pack     5.0
        
        To remove duplicates on specific column(s), use ``subset``.
        
        >>> df.drop_duplicates(subset=['brand'])
            brand style  rating
        0  Yum Yum   cup     4.0
        2  Indomie   cup     3.5
        
        To remove duplicates and keep last occurrences, use ``keep``.
        
        >>> df.drop_duplicates(subset=['brand', 'style'], keep='last')
            brand style  rating
        1  Yum Yum   cup     4.0
        2  Indomie   cup     3.5
        4  Indomie  pack     5.0
    



```

```


```
frame4 = frame3.drop_duplicates()
frame4
```





  <div id="df-726b148c-93c9-4c8b-85a4-3cde381a8a6b">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>column 1</th>
      <th>column 2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Looping</td>
      <td>10</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Looping</td>
      <td>22</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Functions</td>
      <td>23</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Functions</td>
      <td>24</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-726b148c-93c9-4c8b-85a4-3cde381a8a6b')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-726b148c-93c9-4c8b-85a4-3cde381a8a6b button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-726b148c-93c9-4c8b-85a4-3cde381a8a6b');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```
frame3['column 3'] = range(7)
#Let's see the result if we try to drop duplicates 
frame5 = frame3.drop_duplicates()
frame5
```





  <div id="df-ec973251-3814-46da-a94a-b495ccc6260c">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>column 1</th>
      <th>column 2</th>
      <th>column 3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Looping</td>
      <td>10</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Looping</td>
      <td>10</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Looping</td>
      <td>22</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Functions</td>
      <td>23</td>
      <td>3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Functions</td>
      <td>23</td>
      <td>4</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Functions</td>
      <td>24</td>
      <td>5</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Functions</td>
      <td>24</td>
      <td>6</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-ec973251-3814-46da-a94a-b495ccc6260c')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-ec973251-3814-46da-a94a-b495ccc6260c button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-ec973251-3814-46da-a94a-b495ccc6260c');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```
# We can drop rows by passing in column to be checked for duplicate values
frame3['column 3'] = range(7)
frame5 = frame3.drop_duplicates(['column 2'])
frame5
```





  <div id="df-d98ab52e-89e4-4206-94dc-5ebcff9cea9c">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>column 1</th>
      <th>column 2</th>
      <th>column 3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Looping</td>
      <td>10</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Looping</td>
      <td>22</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Functions</td>
      <td>23</td>
      <td>3</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Functions</td>
      <td>24</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-d98ab52e-89e4-4206-94dc-5ebcff9cea9c')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-d98ab52e-89e4-4206-94dc-5ebcff9cea9c button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-d98ab52e-89e4-4206-94dc-5ebcff9cea9c');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




##2.2.2 Exercise


```
"""
Exercise: Drop all duplicates from frame3 using bool series
"""
frame3['column 3'] = range(7)

"""
Solution:
bool_series = frame3["column 2"].duplicated(keep = False)
print(bool_series)
frame5 = frame3[~bool_series]
print(frame5)
"""
```

    0     True
    1     True
    2    False
    3     True
    4     True
    5     True
    6     True
    Name: column 2, dtype: bool
      column 1  column 2  column 3
    2  Looping        22         2


##2.2.3 Exercise


```
"""
Exercise: Keep duplicates from frame3 using bool series, 
          drop the first occurance of duplicate values
"""
frame3['column 3'] = range(7)

"""
Solution
bool_series = frame3["column 2"].duplicated(keep ='last')
print(bool_series)
frame5 = frame3[~bool_series]
print(frame5)
"""
```

    0     True
    1    False
    2    False
    3     True
    4    False
    5     True
    6    False
    Name: column 2, dtype: bool
        column 1  column 2  column 3
    1    Looping        10         1
    2    Looping        22         2
    4  Functions        23         4
    6  Functions        24         6


## 2.2.4 Exercise


```
# Given a DataFrame
df = pd.DataFrame({
         'brand': ['Yum Yum', 'Yum Yum', 'Indomie', 'Indomie', 'Indomie'],
         'style': ['cup', 'cup', 'cup', 'pack', 'pack'],
         'rating': [4, 4, 3.5, 15, 5]
    })
df
```





  <div id="df-ea59ac61-dd33-407f-9c11-49fc17988ffc">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>brand</th>
      <th>style</th>
      <th>rating</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Yum Yum</td>
      <td>cup</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Yum Yum</td>
      <td>cup</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Indomie</td>
      <td>cup</td>
      <td>3.5</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Indomie</td>
      <td>pack</td>
      <td>15.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Indomie</td>
      <td>pack</td>
      <td>5.0</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-ea59ac61-dd33-407f-9c11-49fc17988ffc')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-ea59ac61-dd33-407f-9c11-49fc17988ffc button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-ea59ac61-dd33-407f-9c11-49fc17988ffc');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```
'''
Exercise :
Remove duplicates specifically on 'Brand' column

Solution :
df.drop_duplicates(subset=['brand'])
'''

```





  <div id="df-e23143ce-9a40-4535-97aa-c33d05afa239">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>brand</th>
      <th>style</th>
      <th>rating</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Yum Yum</td>
      <td>cup</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Indomie</td>
      <td>cup</td>
      <td>3.5</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-e23143ce-9a40-4535-97aa-c33d05afa239')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-e23143ce-9a40-4535-97aa-c33d05afa239 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-e23143ce-9a40-4535-97aa-c33d05afa239');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




## 2.2.5 Exercise


```
'''
Exercise :
Remove duplicates and keep last occurrences from the columns of 'Brand' and 'Style'

Solution :
df.drop_duplicates(subset=['brand', 'style'], keep='last')
'''

```

#2.3 Replacing values


```
import numpy as np

```


```
replaceFrame = pd.DataFrame({'column 1': [200., 3000., -786., 3000., 234., 444., -786., 332., 3332. ], 'column 2': range(9)})
replaceFrame.replace(to_replace =-786, value= np.nan)

```





  <div id="df-ae69ddad-dc8f-4663-893a-e4f4ddb7a628">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>column 1</th>
      <th>column 2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>200.0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3000.0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3000.0</td>
      <td>3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>234.0</td>
      <td>4</td>
    </tr>
    <tr>
      <th>5</th>
      <td>444.0</td>
      <td>5</td>
    </tr>
    <tr>
      <th>6</th>
      <td>NaN</td>
      <td>6</td>
    </tr>
    <tr>
      <th>7</th>
      <td>332.0</td>
      <td>7</td>
    </tr>
    <tr>
      <th>8</th>
      <td>3332.0</td>
      <td>8</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-ae69ddad-dc8f-4663-893a-e4f4ddb7a628')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-ae69ddad-dc8f-4663-893a-e4f4ddb7a628 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-ae69ddad-dc8f-4663-893a-e4f4ddb7a628');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




##2.3.1 Exercise


```
replaceFrame = pd.DataFrame({'column 1': [200., 3000., -786., 3000., 234., 444., -786., 332., 3332. ], 'column 2': range(9)})
"""
Exercise: Replace -786 with NaN & 0 with 2
"""

"""
Solution
replaceFrame.replace(to_replace =[-786, 0], value= [np.nan, 2])
"""
```





  <div id="df-7890dd12-2502-4cfe-88ec-0939498e8c63">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>column 1</th>
      <th>column 2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>200.0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3000.0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3000.0</td>
      <td>3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>234.0</td>
      <td>4</td>
    </tr>
    <tr>
      <th>5</th>
      <td>444.0</td>
      <td>5</td>
    </tr>
    <tr>
      <th>6</th>
      <td>NaN</td>
      <td>6</td>
    </tr>
    <tr>
      <th>7</th>
      <td>332.0</td>
      <td>7</td>
    </tr>
    <tr>
      <th>8</th>
      <td>3332.0</td>
      <td>8</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-7890dd12-2502-4cfe-88ec-0939498e8c63')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-7890dd12-2502-4cfe-88ec-0939498e8c63 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-7890dd12-2502-4cfe-88ec-0939498e8c63');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




##2.3.2 Exercise

Find and replace the missing values in a given DataFrame which do not have any valuable information.

Example:
Missing values: ?, --
Replace those values with NaN



```
ord_no purch_amt    ord_date customer_id salesman_id
0   70001     150.5           ?        3002        5002
1     NaN    270.65  2012-09-10        3001        5003
2   70002     65.26         NaN        3001           ?
3   70004     110.5  2012-08-17        3003        5001
4     NaN     948.5  2012-09-10        3002         NaN
5   70005    2400.6  2012-07-27        3001        5002
6      --      5760  2012-09-10        3001        5001
7   70010         ?  2012-10-10        3004           ?
8   70003     12.43  2012-10-10          --        5003
9   70012    2480.4  2012-06-27        3002        5002
10    NaN    250.45  2012-08-17        3001        5003
11  70013    3045.6  2012-04-25        3001          --
```


```
import pandas as pd
import numpy as np
pd.set_option('display.max_rows', None)
#pd.set_option('display.max_columns', None)

df = pd.DataFrame({
'ord_no':[70001,np.nan,70002,70004,np.nan,70005,"--",70010,70003,70012,np.nan,70013],
'purch_amt':[150.5,270.65,65.26,110.5,948.5,2400.6,5760,"?",12.43,2480.4,250.45, 3045.6],
'ord_date': ['?','2012-09-10',np.nan,'2012-08-17','2012-09-10','2012-07-27','2012-09-10','2012-10-10','2012-10-10','2012-06-27','2012-08-17','2012-04-25'],
'customer_id':[3002,3001,3001,3003,3002,3001,3001,3004,"--",3002,3001,3001],
'salesman_id':[5002,5003,"?",5001,np.nan,5002,5001,"?",5003,5002,5003,"--"]})

```


```
# Solution
'''
result = df.replace({"?": np.nan, "--": np.nan})
print(result)
'''
```

##2.3.3 Exercise

Replace NaNs with a single constant value in specified columns in a DataFrame.

```
ord_no purch_amt    ord_date customer_id salesman_id
0   70001     150.5           ?        3002        5002
1     NaN    270.65  2012-09-10        3001        5003
2   70002     65.26         NaN        3001           ?
3   70004     110.5  2012-08-17        3003        5001
4     NaN     948.5  2012-09-10        3002         NaN
5   70005    2400.6  2012-07-27        3001        5002
6      --      5760  2012-09-10        3001        5001
7   70010         ?  2012-10-10        3004           ?
8   70003     12.43  2012-10-10          --        5003
9   70012    2480.4  2012-06-27        3002        5002
10    NaN    250.45  2012-08-17        3001        5003
11  70013    3045.6  2012-04-25        3001          --
```


```
import pandas as pd
import numpy as np
pd.set_option('display.max_rows', None)
#pd.set_option('display.max_columns', None)

df = pd.DataFrame({
'ord_no':[70001,np.nan,70002,70004,np.nan,70005,"--",70010,70003,70012,np.nan,70013],
'purch_amt':[150.5,270.65,65.26,110.5,948.5,2400.6,5760,"?",12.43,2480.4,250.45, 3045.6],
'ord_date': ['?','2012-09-10',np.nan,'2012-08-17','2012-09-10','2012-07-27','2012-09-10','2012-10-10','2012-10-10','2012-06-27','2012-08-17','2012-04-25'],
'customer_id':[3002,3001,3001,3003,3002,3001,3001,3004,"--",3002,3001,3001],
'salesman_id':[5002,5003,"?",5001,np.nan,5002,5001,"?",5003,5002,5003,"--"]})
```


```
# Solution

'''
result = df['ord_no'].fillna(0, inplace=False)
print(result)
'''
```

##2.3.4 Exercise

Replace NaNs with the value from the previous row or the next row in a given DataFrame.
```
ord_no purch_amt    ord_date customer_id salesman_id
0   70001     150.5           ?        3002        5002
1     NaN    270.65  2012-09-10        3001        5003
2   70002     65.26         NaN        3001           ?
3   70004     110.5  2012-08-17        3003        5001
4     NaN     948.5  2012-09-10        3002         NaN
5   70005    2400.6  2012-07-27        3001        5002
6      --      5760  2012-09-10        3001        5001
7   70010         ?  2012-10-10        3004           ?
8   70003     12.43  2012-10-10          --        5003
9   70012    2480.4  2012-06-27        3002        5002
10    NaN    250.45  2012-08-17        3001        5003
11  70013    3045.6  2012-04-25        3001          --
```


```
import pandas as pd
import numpy as np
pd.set_option('display.max_rows', None)
#pd.set_option('display.max_columns', None)

df = pd.DataFrame({
'ord_no':[70001,np.nan,70002,70004,np.nan,70005,"--",70010,70003,70012,np.nan,70013],
'purch_amt':[150.5,270.65,65.26,110.5,948.5,2400.6,5760,"?",12.43,2480.4,250.45, 3045.6],
'ord_date': ['?','2012-09-10',np.nan,'2012-08-17','2012-09-10','2012-07-27','2012-09-10','2012-10-10','2012-10-10','2012-06-27','2012-08-17','2012-04-25'],
'customer_id':[3002,3001,3001,3003,3002,3001,3001,3004,"--",3002,3001,3001],
'salesman_id':[5002,5003,"?",5001,np.nan,5002,5001,"?",5003,5002,5003,"--"]})
```


```
# Solution
'''
df['sale_amt'].fillna(method='bfill', inplace=True)
print(df)
'''
```

##2.3.5 Exercise

Replace NaNs with the value from the previous row or the next row in a given DataFrame.
```
ord_no purch_amt    ord_date customer_id salesman_id
0   70001     150.5           ?        3002        5002
1     NaN    270.65  2012-09-10        3001        5003
2   70002     65.26         NaN        3001           ?
3   70004     110.5  2012-08-17        3003        5001
4     NaN     948.5  2012-09-10        3002         NaN
5   70005    2400.6  2012-07-27        3001        5002
6      --      5760  2012-09-10        3001        5001
7   70010         ?  2012-10-10        3004           ?
8   70003     12.43  2012-10-10          --        5003
9   70012    2480.4  2012-06-27        3002        5002
10    NaN    250.45  2012-08-17        3001        5003
11  70013    3045.6  2012-04-25        3001          --
```


```
import pandas as pd
import numpy as np
pd.set_option('display.max_rows', None)
#pd.set_option('display.max_columns', None)

df = pd.DataFrame({
'ord_no':[70001,np.nan,70002,70004,np.nan,70005,"--",70010,70003,70012,np.nan,70013],
'purch_amt':[150.5,270.65,65.26,110.5,948.5,2400.6,5760,"?",12.43,2480.4,250.45, 3045.6],
'ord_date': ['?','2012-09-10',np.nan,'2012-08-17','2012-09-10','2012-07-27','2012-09-10','2012-10-10','2012-10-10','2012-06-27','2012-08-17','2012-04-25'],
'customer_id':[3002,3001,3001,3003,3002,3001,3001,3004,"--",3002,3001,3001],
'salesman_id':[5002,5003,"?",5001,np.nan,5002,5001,"?",5003,5002,5003,"--"]})
```


```
# Solution
df['purch_amt'].fillna(df['purch_amt'].median(), inplace=True)
print(df)
print("Using mean to replace NaN:")
df['sale_amt'].fillna(int(df['sale_amt'].mean()), inplace=True)
print(df)
```

# 2.4 Handling missing data


```
data = np.arange(15, 30).reshape(5, 3)
df_store = pd.DataFrame(data, index=['apple', 'banana', 'kiwi', 'grapes', 'mango'], columns=['store1', 'store2', 'store3'])
df_store
```





  <div id="df-6e4839d4-8c70-4981-a1bd-1df6c4880218">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>store1</th>
      <th>store2</th>
      <th>store3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>apple</th>
      <td>15</td>
      <td>16</td>
      <td>17</td>
    </tr>
    <tr>
      <th>banana</th>
      <td>18</td>
      <td>19</td>
      <td>20</td>
    </tr>
    <tr>
      <th>kiwi</th>
      <td>21</td>
      <td>22</td>
      <td>23</td>
    </tr>
    <tr>
      <th>grapes</th>
      <td>24</td>
      <td>25</td>
      <td>26</td>
    </tr>
    <tr>
      <th>mango</th>
      <td>27</td>
      <td>28</td>
      <td>29</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-6e4839d4-8c70-4981-a1bd-1df6c4880218')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-6e4839d4-8c70-4981-a1bd-1df6c4880218 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-6e4839d4-8c70-4981-a1bd-1df6c4880218');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```
df_store['store4'] = np.nan
df_store.loc['watermelon'] = np.arange(15, 19)
df_store.loc['oranges'] = np.nan
df_store['store5'] = np.nan
df_store['store4']['apple'] = 20.
df_store
```





  <div id="df-2b9ecf7b-70a1-441a-9bb0-241d098cdb2c">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>store1</th>
      <th>store2</th>
      <th>store3</th>
      <th>store4</th>
      <th>store5</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>apple</th>
      <td>15.0</td>
      <td>16.0</td>
      <td>17.0</td>
      <td>20.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>banana</th>
      <td>18.0</td>
      <td>19.0</td>
      <td>20.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>kiwi</th>
      <td>21.0</td>
      <td>22.0</td>
      <td>23.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>grapes</th>
      <td>24.0</td>
      <td>25.0</td>
      <td>26.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>mango</th>
      <td>27.0</td>
      <td>28.0</td>
      <td>29.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>watermelon</th>
      <td>15.0</td>
      <td>16.0</td>
      <td>17.0</td>
      <td>18.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>oranges</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-2b9ecf7b-70a1-441a-9bb0-241d098cdb2c')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-2b9ecf7b-70a1-441a-9bb0-241d098cdb2c button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-2b9ecf7b-70a1-441a-9bb0-241d098cdb2c');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```
df_store.isnull()
```





  <div id="df-ed17fdc0-1897-4fbd-88fc-caeae4006209">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>store1</th>
      <th>store2</th>
      <th>store3</th>
      <th>store4</th>
      <th>store5</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>apple</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>banana</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>kiwi</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>grapes</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>mango</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>watermelon</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>oranges</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-ed17fdc0-1897-4fbd-88fc-caeae4006209')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-ed17fdc0-1897-4fbd-88fc-caeae4006209 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-ed17fdc0-1897-4fbd-88fc-caeae4006209');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




##2.4.1 Exercise


```
"""
Exercise: Check for non null values in df_store
"""

"""
Solution
df_store.notnull()
"""
```





  <div id="df-6085dff8-446b-406f-9876-43f94bc540c3">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>store1</th>
      <th>store2</th>
      <th>store3</th>
      <th>store4</th>
      <th>store5</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>apple</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
    </tr>
    <tr>
      <th>banana</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>kiwi</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>grapes</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>mango</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>watermelon</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
    </tr>
    <tr>
      <th>oranges</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-6085dff8-446b-406f-9876-43f94bc540c3')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-6085dff8-446b-406f-9876-43f94bc540c3 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-6085dff8-446b-406f-9876-43f94bc540c3');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```
df_store.isnull().sum()
```




    store1    1
    store2    1
    store3    1
    store4    5
    store5    7
    dtype: int64



## 2.4.2 Exercise Find All Null Values



```
"""
Exercise: Return sum of ALL null values in df_store
"""

"""
Solution
df_store.isnull().sum().sum()
"""
```




    15




```
df_store.count()
```




    store1    6
    store2    6
    store3    6
    store4    2
    store5    0
    dtype: int64




```
"""
Exercise: Return ALL non null values in "store4" of df_store
"""

"""
Solution
df_store.store4[df_store.store4.notnull()]
"""
```




    apple         20.0
    watermelon    18.0
    Name: store4, dtype: float64




```
df_store.store4.dropna()

```




    apple         20.0
    watermelon    18.0
    Name: store4, dtype: float64




```
df_store.dropna()
```





  <div id="df-27dd92d2-e2b4-4e15-a538-0d9ad618393b">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>store1</th>
      <th>store2</th>
      <th>store3</th>
      <th>store4</th>
      <th>store5</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-27dd92d2-e2b4-4e15-a538-0d9ad618393b')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-27dd92d2-e2b4-4e15-a538-0d9ad618393b button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-27dd92d2-e2b4-4e15-a538-0d9ad618393b');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```
"""
Exercise: Drop rows with ALL null values in df_store
"""

"""
Solution
df_store.dropna(how='all')
"""
```





  <div id="df-888f56c1-d318-4d67-9872-bff01f352e91">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>store1</th>
      <th>store2</th>
      <th>store3</th>
      <th>store4</th>
      <th>store5</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>apple</th>
      <td>15.0</td>
      <td>16.0</td>
      <td>17.0</td>
      <td>20.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>banana</th>
      <td>18.0</td>
      <td>19.0</td>
      <td>20.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>kiwi</th>
      <td>21.0</td>
      <td>22.0</td>
      <td>23.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>grapes</th>
      <td>24.0</td>
      <td>25.0</td>
      <td>26.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>mango</th>
      <td>27.0</td>
      <td>28.0</td>
      <td>29.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>watermelon</th>
      <td>15.0</td>
      <td>16.0</td>
      <td>17.0</td>
      <td>18.0</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-888f56c1-d318-4d67-9872-bff01f352e91')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-888f56c1-d318-4d67-9872-bff01f352e91 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-888f56c1-d318-4d67-9872-bff01f352e91');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```
"""
Exercise: Drop columns with ALL null values in df_store
"""

"""
Solution
df_store.dropna(how='all', axis=1)
"""
```





  <div id="df-13199dd5-3cfb-470c-a536-85f34353a92a">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>store1</th>
      <th>store2</th>
      <th>store3</th>
      <th>store4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>apple</th>
      <td>15.0</td>
      <td>16.0</td>
      <td>17.0</td>
      <td>20.0</td>
    </tr>
    <tr>
      <th>banana</th>
      <td>18.0</td>
      <td>19.0</td>
      <td>20.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>kiwi</th>
      <td>21.0</td>
      <td>22.0</td>
      <td>23.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>grapes</th>
      <td>24.0</td>
      <td>25.0</td>
      <td>26.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>mango</th>
      <td>27.0</td>
      <td>28.0</td>
      <td>29.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>watermelon</th>
      <td>15.0</td>
      <td>16.0</td>
      <td>17.0</td>
      <td>18.0</td>
    </tr>
    <tr>
      <th>oranges</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-13199dd5-3cfb-470c-a536-85f34353a92a')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-13199dd5-3cfb-470c-a536-85f34353a92a button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-13199dd5-3cfb-470c-a536-85f34353a92a');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```
df_store2 = df_store.copy()
df_store2.loc['oranges'].store1 = 0
df_store2.loc['oranges'].store3 = 0
df_store2
```





  <div id="df-6a9dbc3c-dfe7-4acb-98cb-8eadab60598d">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>store1</th>
      <th>store2</th>
      <th>store3</th>
      <th>store4</th>
      <th>store5</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>apple</th>
      <td>15.0</td>
      <td>16.0</td>
      <td>17.0</td>
      <td>20.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>banana</th>
      <td>18.0</td>
      <td>19.0</td>
      <td>20.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>kiwi</th>
      <td>21.0</td>
      <td>22.0</td>
      <td>23.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>grapes</th>
      <td>24.0</td>
      <td>25.0</td>
      <td>26.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>mango</th>
      <td>27.0</td>
      <td>28.0</td>
      <td>29.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>watermelon</th>
      <td>15.0</td>
      <td>16.0</td>
      <td>17.0</td>
      <td>18.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>oranges</th>
      <td>0.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-6a9dbc3c-dfe7-4acb-98cb-8eadab60598d')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-6a9dbc3c-dfe7-4acb-98cb-8eadab60598d button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-6a9dbc3c-dfe7-4acb-98cb-8eadab60598d');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```
df_store2.dropna(how='any', axis=1)
```





  <div id="df-d2773e79-35dd-44f5-b748-ae1cfcb50dc4">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>store1</th>
      <th>store3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>apple</th>
      <td>15.0</td>
      <td>17.0</td>
    </tr>
    <tr>
      <th>banana</th>
      <td>18.0</td>
      <td>20.0</td>
    </tr>
    <tr>
      <th>kiwi</th>
      <td>21.0</td>
      <td>23.0</td>
    </tr>
    <tr>
      <th>grapes</th>
      <td>24.0</td>
      <td>26.0</td>
    </tr>
    <tr>
      <th>mango</th>
      <td>27.0</td>
      <td>29.0</td>
    </tr>
    <tr>
      <th>watermelon</th>
      <td>15.0</td>
      <td>17.0</td>
    </tr>
    <tr>
      <th>oranges</th>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-d2773e79-35dd-44f5-b748-ae1cfcb50dc4')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-d2773e79-35dd-44f5-b748-ae1cfcb50dc4 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-d2773e79-35dd-44f5-b748-ae1cfcb50dc4');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```
"""
Exercise: Drop columns with alteast 5 null values 
"""

"""
Solution
df_store.dropna(thresh=5, axis=1)
"""
```





  <div id="df-673dde3f-453f-47da-813b-a34197e42857">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>store1</th>
      <th>store2</th>
      <th>store3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>apple</th>
      <td>15.0</td>
      <td>16.0</td>
      <td>17.0</td>
    </tr>
    <tr>
      <th>banana</th>
      <td>18.0</td>
      <td>19.0</td>
      <td>20.0</td>
    </tr>
    <tr>
      <th>kiwi</th>
      <td>21.0</td>
      <td>22.0</td>
      <td>23.0</td>
    </tr>
    <tr>
      <th>grapes</th>
      <td>24.0</td>
      <td>25.0</td>
      <td>26.0</td>
    </tr>
    <tr>
      <th>mango</th>
      <td>27.0</td>
      <td>28.0</td>
      <td>29.0</td>
    </tr>
    <tr>
      <th>watermelon</th>
      <td>15.0</td>
      <td>16.0</td>
      <td>17.0</td>
    </tr>
    <tr>
      <th>oranges</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-673dde3f-453f-47da-813b-a34197e42857')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-673dde3f-453f-47da-813b-a34197e42857 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-673dde3f-453f-47da-813b-a34197e42857');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




##2.4.3 NaN values in mathematical operations


```
ar1 = np.array([100, 200, np.nan, 300])
ser1 = pd.Series(ar1)

ar1.mean(), ser1.mean()
```




    (nan, 200.0)




```
ser2 = df_store.store4
ser2.sum()
```




    38.0




```
ser2.mean()
```




    19.0




```
ser2.cumsum()
```




    apple         20.0
    banana         NaN
    kiwi           NaN
    grapes         NaN
    mango          NaN
    watermelon    38.0
    oranges        NaN
    Name: store4, dtype: float64



##2.4.4 Exercise


```
"""
Exercise: Add 1 to all non null values of store4 in df_store
"""

"""
Solution
df_store.store4 + 1
"""
```




    apple         21.0
    banana         NaN
    kiwi           NaN
    grapes         NaN
    mango          NaN
    watermelon    19.0
    oranges        NaN
    Name: store4, dtype: float64



##2.4.5 Exercise

Program to detect missing values of a given DataFrame. Display True or False.
```
     ord_no  purch_amt    ord_date  customer_id  salesman_id
0   70001.0     150.50  2012-10-05         3002       5002.0
1       NaN     270.65  2012-09-10         3001       5003.0
2   70002.0      65.26         NaN         3001       5001.0
3   70004.0     110.50  2012-08-17         3003          NaN
4       NaN     948.50  2012-09-10         3002       5002.0
5   70005.0    2400.60  2012-07-27         3001       5001.0
6       NaN    5760.00  2012-09-10         3001       5001.0
7   70010.0    1983.43  2012-10-10         3004          NaN
8   70003.0    2480.40  2012-10-10         3003       5003.0
9   70012.0     250.45  2012-06-27         3002       5002.0
10      NaN      75.29  2012-08-17         3001       5003.0
11  70013.0    3045.60  2012-04-25         3001          NaN

```


```
import pandas as pd
import numpy as np
pd.set_option('display.max_rows', None)
#pd.set_option('display.max_columns', None)

df = pd.DataFrame({
'ord_no':[70001,np.nan,70002,70004,np.nan,70005,np.nan,70010,70003,70012,np.nan,70013],
'purch_amt':[150.5,270.65,65.26,110.5,948.5,2400.6,5760,1983.43,2480.4,250.45, 75.29,3045.6],
'ord_date': ['2012-10-05','2012-09-10',np.nan,'2012-08-17','2012-09-10','2012-07-27','2012-09-10','2012-10-10','2012-10-10','2012-06-27','2012-08-17','2012-04-25'],
'customer_id':[3002,3001,3001,3003,3002,3001,3001,3004,3003,3002,3001,3001],
'salesman_id':[5002,5003,5001,np.nan,5002,5001,5001,np.nan,5003,5002,5003,np.nan]})

'''
print("\nMissing values of the said dataframe:")
print(df.isna())
'''
```

#2.5 Filling in missing data



```
filledDf = df_store.fillna(0)
filledDf
```





  <div id="df-f6a4dc26-110b-4ca3-880b-f2e40112f667">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>store1</th>
      <th>store2</th>
      <th>store3</th>
      <th>store4</th>
      <th>store5</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>apple</th>
      <td>15.0</td>
      <td>16.0</td>
      <td>17.0</td>
      <td>20.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>banana</th>
      <td>18.0</td>
      <td>19.0</td>
      <td>20.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>kiwi</th>
      <td>21.0</td>
      <td>22.0</td>
      <td>23.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>grapes</th>
      <td>24.0</td>
      <td>25.0</td>
      <td>26.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>mango</th>
      <td>27.0</td>
      <td>28.0</td>
      <td>29.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>watermelon</th>
      <td>15.0</td>
      <td>16.0</td>
      <td>17.0</td>
      <td>18.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>oranges</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-f6a4dc26-110b-4ca3-880b-f2e40112f667')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-f6a4dc26-110b-4ca3-880b-f2e40112f667 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-f6a4dc26-110b-4ca3-880b-f2e40112f667');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```
df_store.mean()
```




    store1    20.0
    store2    21.0
    store3    22.0
    store4    19.0
    store5     NaN
    dtype: float64



## 2.5.1 Exercise


```
"""
Exercise: Calculate mean of all stores in filledDf
"""

"""
Solution
filledDf.mean()
"""
```




    store1    17.142857
    store2    18.000000
    store3    18.857143
    store4     5.428571
    store5     0.000000
    dtype: float64



##2.5.2 Forward and backward filling of the missing values


```
df_store.store4.fillna(method='ffill')
```




    apple         20.0
    banana        20.0
    kiwi          20.0
    grapes        20.0
    mango         20.0
    watermelon    18.0
    oranges       18.0
    Name: store4, dtype: float64




```
df_store.store4.fillna(method='bfill')
```




    apple         20.0
    banana        18.0
    kiwi          18.0
    grapes        18.0
    mango         18.0
    watermelon    18.0
    oranges        NaN
    Name: store4, dtype: float64



##2.5.3 Filling with index labels



```
to_fill = pd.Series([14, 23, 12], index=['apple', 'mango', 'oranges'])
to_fill
```




    apple      14
    mango      23
    oranges    12
    dtype: int64




```
df_store.store4.fillna(to_fill)

```




    '\nSolution\ndf_store.store4.fillna(to_fill)\n'




```
df_store.mean()
```




    store1    20.0
    store2    21.0
    store3    22.0
    store4    19.0
    store5     NaN
    dtype: float64



##2.5.4 Exercise


```
"""
Exercise: Use mean of each store in df_store to populate respective null values in the columns
"""
df_store.fillna(df_store.mean())
```





  <div id="df-63492c4f-2329-4b7c-aef8-badbb4bbd04b">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>store1</th>
      <th>store2</th>
      <th>store3</th>
      <th>store4</th>
      <th>store5</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>apple</th>
      <td>15.0</td>
      <td>16.0</td>
      <td>17.0</td>
      <td>20.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>banana</th>
      <td>18.0</td>
      <td>19.0</td>
      <td>20.0</td>
      <td>19.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>kiwi</th>
      <td>21.0</td>
      <td>22.0</td>
      <td>23.0</td>
      <td>19.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>grapes</th>
      <td>24.0</td>
      <td>25.0</td>
      <td>26.0</td>
      <td>19.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>mango</th>
      <td>27.0</td>
      <td>28.0</td>
      <td>29.0</td>
      <td>19.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>watermelon</th>
      <td>15.0</td>
      <td>16.0</td>
      <td>17.0</td>
      <td>18.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>oranges</th>
      <td>20.0</td>
      <td>21.0</td>
      <td>22.0</td>
      <td>19.0</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-63492c4f-2329-4b7c-aef8-badbb4bbd04b')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-63492c4f-2329-4b7c-aef8-badbb4bbd04b button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-63492c4f-2329-4b7c-aef8-badbb4bbd04b');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




##2.5.5 Interpolation of missing values


```
ser3 = pd.Series([100, np.nan, np.nan, np.nan, 292])
ser3.interpolate()
```




    0    100.0
    1    148.0
    2    196.0
    3    244.0
    4    292.0
    dtype: float64




```
from datetime import datetime
ts = pd.Series([10, np.nan, np.nan, 9], 
               index=[datetime(2019, 1,1), 
                      datetime(2019, 2,1), 
                      datetime(2019, 3,1),
                      datetime(2019, 5,1)])

ts
```




    2019-01-01    10.0
    2019-02-01     NaN
    2019-03-01     NaN
    2019-05-01     9.0
    dtype: float64




```
"""
Exercise: Use interpolate() to fill ts
"""

"""
Solution
ts.interpolate()
"""
```




    2019-01-01    10.000000
    2019-02-01     9.666667
    2019-03-01     9.333333
    2019-05-01     9.000000
    dtype: float64




```
ts.interpolate(method='time')
```




    2019-01-01    10.000000
    2019-02-01     9.741667
    2019-03-01     9.508333
    2019-05-01     9.000000
    dtype: float64



#2.6 Renaming axis indexes


```
import numpy as np
import pandas as pd
data = np.arange(15).reshape((3,5))
indexers = ['Rainfall', 'Humidity', 'Wind']
dframe1 = pd.DataFrame(data, index=indexers, columns=['Lucknow', 'Delhi', 'Bengaluru', 'Chennai', 'Kolkata'])
dframe1
```





  <div id="df-ae774441-9f7b-4b1c-84be-07aa09728398">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Lucknow</th>
      <th>Delhi</th>
      <th>Bengaluru</th>
      <th>Chennai</th>
      <th>Kolkata</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Rainfall</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>Humidity</th>
      <td>5</td>
      <td>6</td>
      <td>7</td>
      <td>8</td>
      <td>9</td>
    </tr>
    <tr>
      <th>Wind</th>
      <td>10</td>
      <td>11</td>
      <td>12</td>
      <td>13</td>
      <td>14</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-ae774441-9f7b-4b1c-84be-07aa09728398')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-ae774441-9f7b-4b1c-84be-07aa09728398 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-ae774441-9f7b-4b1c-84be-07aa09728398');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```
# Say, you want to transform the index terms to capital letter. 

dframe1.index = dframe1.index.map(str.upper)
dframe1
```





  <div id="df-78564122-66e6-49f9-9985-d413a5ea8fe8">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Lucknow</th>
      <th>Delhi</th>
      <th>Bengaluru</th>
      <th>Chennai</th>
      <th>Kolkata</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>RAINFALL</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>HUMIDITY</th>
      <td>5</td>
      <td>6</td>
      <td>7</td>
      <td>8</td>
      <td>9</td>
    </tr>
    <tr>
      <th>WIND</th>
      <td>10</td>
      <td>11</td>
      <td>12</td>
      <td>13</td>
      <td>14</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-78564122-66e6-49f9-9985-d413a5ea8fe8')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-78564122-66e6-49f9-9985-d413a5ea8fe8 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-78564122-66e6-49f9-9985-d413a5ea8fe8');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




##2.6.1 Exercise


```
"""
Exercise: Rename dframe1 index to Title Case & Column Names to Capital/Upper Case
"""

"""
Solution
dframe1.rename(index=str.title, columns=str.upper)
"""
```





  <div id="df-e11c4a51-0b78-4a20-b807-31a99fb8d6b4">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>LUCKNOW</th>
      <th>DELHI</th>
      <th>BENGALURU</th>
      <th>CHENNAI</th>
      <th>KOLKATA</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Rainfall</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>Humidity</th>
      <td>5</td>
      <td>6</td>
      <td>7</td>
      <td>8</td>
      <td>9</td>
    </tr>
    <tr>
      <th>Wind</th>
      <td>10</td>
      <td>11</td>
      <td>12</td>
      <td>13</td>
      <td>14</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-e11c4a51-0b78-4a20-b807-31a99fb8d6b4')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-e11c4a51-0b78-4a20-b807-31a99fb8d6b4 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-e11c4a51-0b78-4a20-b807-31a99fb8d6b4');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




## 2.6.2 Exercise


```
'''
Exercise : Try using inplace = True. What is the difference/significance of this command?
'''

'''
Solution
dframe1.rename(index=str.title, columns=str.upper, inplace = True)
'''
```

## 2.6.3 Exercise


```
df = pd.DataFrame({"A": [1, 2, 3], "B": [4, 5, 6]})
```


```
'''
Rename the indices of the dataframe mentioned above.
'''

'''
Solution
df.rename(index={0: "x", 1: "y", 2: "z"})
'''
```




    '\nSolution\ndf.rename(index={0: "x", 1: "y", 2: "z"})\n'



## 2.6.4 Exercise


```
'''
Rename the indices 1 as 2 and 2 as 4
'''

'''
df.rename({1: 2, 2: 4}, axis='index')
'''
```

##2.6.5 Exercise


```
"""
Exercise: Rename dframe1 index to Lower Case & Column Names to lower Case
"""

"""
Solution
"""
dframe1.rename(index=str.lower, columns=str.lower)

```





  <div id="df-c701d329-0854-4868-a460-a58baef9a37e">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>lucknow</th>
      <th>delhi</th>
      <th>bengaluru</th>
      <th>chennai</th>
      <th>kolkata</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>rainfall</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>humidity</th>
      <td>5</td>
      <td>6</td>
      <td>7</td>
      <td>8</td>
      <td>9</td>
    </tr>
    <tr>
      <th>wind</th>
      <td>10</td>
      <td>11</td>
      <td>12</td>
      <td>13</td>
      <td>14</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-c701d329-0854-4868-a460-a58baef9a37e')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-c701d329-0854-4868-a460-a58baef9a37e button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-c701d329-0854-4868-a460-a58baef9a37e');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




#2.7 Discretization and binning



```
import pandas as pd

height = [120, 122, 125, 127, 121, 123, 137, 131, 161, 145, 141, 132]

bins = [118, 125, 135, 160, 200]

category = pd.cut(height, bins)

category
```




    [(118, 125], (118, 125], (118, 125], (125, 135], (118, 125], ..., (125, 135], (160, 200], (135, 160], (135, 160], (125, 135]]
    Length: 12
    Categories (4, interval[int64, right]): [(118, 125] < (125, 135] < (135, 160] < (160, 200]]



##2.7.1 Exercise


```
"""
Exercise: Get frequency of items in every bin
Hint use value_counts()
"""

"""
Solution
pd.value_counts(category)
"""
```




    '\nSolution\npd.value_counts(category)\n'



##2.7.2 Exercise


```
"""
Exercise: Change the default behaviour of pd.cut() to include 
right value of bin and exclude left 
This would be inverse of its natural behaviour of including left limit and exclude right limit
"""

"""
Solution
category2 = pd.cut(height, [118, 126, 136, 161, 200], right=False)

category2
"""

```




    [[118, 126), [118, 126), [118, 126), [126, 136), [118, 126), ..., [126, 136), [161, 200), [136, 161), [136, 161), [126, 136)]
    Length: 12
    Categories (4, interval[int64, left]): [[118, 126) < [126, 136) < [136, 161) < [161, 200)]



## 2.7.3 Exercise


```
"""
Exercise: Use phrases as bin labels
"""

"""
Solution
bin_names = ['Short Height', 'Averge height', 'Good Height', 'Taller']
pd.cut(height, bins, labels=bin_names)
"""
```




    ['Short Height', 'Short Height', 'Short Height', 'Averge height', 'Short Height', ..., 'Averge height', 'Taller', 'Good Height', 'Good Height', 'Averge height']
    Length: 12
    Categories (4, object): ['Short Height' < 'Averge height' < 'Good Height' < 'Taller']



##2.7.4 Exercise


```
"""
Exercise: Generate 40 numbers from range [0,1] use Integer value as number of bins
Set precision value as 3
"""
import numpy as np

pd.cut(np.random.rand(40), 5, precision=3)

```




    [(0.752, 0.94], (0.752, 0.94], (0.00184, 0.19], (0.377, 0.565], (0.752, 0.94], ..., (0.00184, 0.19], (0.377, 0.565], (0.00184, 0.19], (0.377, 0.565], (0.19, 0.377]]
    Length: 40
    Categories (5, interval[float64, right]): [(0.00184, 0.19] < (0.19, 0.377] < (0.377, 0.565] <
                                               (0.565, 0.752] < (0.752, 0.94]]



##2.7.5 Exercise


```
"""
Generate 50 numerical values between [0,1] and use Qcut to
cut it into quartiles

Qcut (quantile-cut) differs from cut in the sense that, in qcut,
the number of elements in each bin will be roughly the same,
but this will come at the cost of differently sized interval widths.
""" 
randomNumbers = np.random.rand(50)
category3 = pd.qcut(randomNumbers, 4) 
#pd.qcut(randomNumbers, [0, 0.1, 0.5, 0.7, 1.0]) Explicitly bin range
category3
```




    [(0.762, 0.989], (0.267, 0.584], (0.762, 0.989], (0.0423, 0.267], (0.584, 0.762], ..., (0.762, 0.989], (0.267, 0.584], (0.584, 0.762], (0.762, 0.989], (0.584, 0.762]]
    Length: 50
    Categories (4, interval[float64, right]): [(0.0423, 0.267] < (0.267, 0.584] < (0.584, 0.762] <
                                               (0.762, 0.989]]




```
pd.value_counts(category3)
```




    (0.00537, 0.29]    13
    (0.783, 0.989]     13
    (0.29, 0.538]      12
    (0.538, 0.783]     12
    dtype: int64



#2.8 Permunation and Random sampling


```
dat = np.arange(80).reshape(10,8)
df = pd.DataFrame(dat)

df
```





  <div id="df-870fe070-d761-4c7f-9b6e-eda25c20fb1c">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
      <td>4</td>
      <td>5</td>
      <td>6</td>
      <td>7</td>
    </tr>
    <tr>
      <th>1</th>
      <td>8</td>
      <td>9</td>
      <td>10</td>
      <td>11</td>
      <td>12</td>
      <td>13</td>
      <td>14</td>
      <td>15</td>
    </tr>
    <tr>
      <th>2</th>
      <td>16</td>
      <td>17</td>
      <td>18</td>
      <td>19</td>
      <td>20</td>
      <td>21</td>
      <td>22</td>
      <td>23</td>
    </tr>
    <tr>
      <th>3</th>
      <td>24</td>
      <td>25</td>
      <td>26</td>
      <td>27</td>
      <td>28</td>
      <td>29</td>
      <td>30</td>
      <td>31</td>
    </tr>
    <tr>
      <th>4</th>
      <td>32</td>
      <td>33</td>
      <td>34</td>
      <td>35</td>
      <td>36</td>
      <td>37</td>
      <td>38</td>
      <td>39</td>
    </tr>
    <tr>
      <th>5</th>
      <td>40</td>
      <td>41</td>
      <td>42</td>
      <td>43</td>
      <td>44</td>
      <td>45</td>
      <td>46</td>
      <td>47</td>
    </tr>
    <tr>
      <th>6</th>
      <td>48</td>
      <td>49</td>
      <td>50</td>
      <td>51</td>
      <td>52</td>
      <td>53</td>
      <td>54</td>
      <td>55</td>
    </tr>
    <tr>
      <th>7</th>
      <td>56</td>
      <td>57</td>
      <td>58</td>
      <td>59</td>
      <td>60</td>
      <td>61</td>
      <td>62</td>
      <td>63</td>
    </tr>
    <tr>
      <th>8</th>
      <td>64</td>
      <td>65</td>
      <td>66</td>
      <td>67</td>
      <td>68</td>
      <td>69</td>
      <td>70</td>
      <td>71</td>
    </tr>
    <tr>
      <th>9</th>
      <td>72</td>
      <td>73</td>
      <td>74</td>
      <td>75</td>
      <td>76</td>
      <td>77</td>
      <td>78</td>
      <td>79</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-870fe070-d761-4c7f-9b6e-eda25c20fb1c')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-870fe070-d761-4c7f-9b6e-eda25c20fb1c button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-870fe070-d761-4c7f-9b6e-eda25c20fb1c');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```
sampler = np.random.permutation(10)
sampler
```




    array([2, 3, 1, 7, 5, 8, 9, 0, 6, 4])




```
df.take(sampler)
```





  <div id="df-dc43912a-3894-422d-a00e-5c0d59efce06">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>16</td>
      <td>17</td>
      <td>18</td>
      <td>19</td>
      <td>20</td>
      <td>21</td>
      <td>22</td>
      <td>23</td>
    </tr>
    <tr>
      <th>3</th>
      <td>24</td>
      <td>25</td>
      <td>26</td>
      <td>27</td>
      <td>28</td>
      <td>29</td>
      <td>30</td>
      <td>31</td>
    </tr>
    <tr>
      <th>1</th>
      <td>8</td>
      <td>9</td>
      <td>10</td>
      <td>11</td>
      <td>12</td>
      <td>13</td>
      <td>14</td>
      <td>15</td>
    </tr>
    <tr>
      <th>7</th>
      <td>56</td>
      <td>57</td>
      <td>58</td>
      <td>59</td>
      <td>60</td>
      <td>61</td>
      <td>62</td>
      <td>63</td>
    </tr>
    <tr>
      <th>5</th>
      <td>40</td>
      <td>41</td>
      <td>42</td>
      <td>43</td>
      <td>44</td>
      <td>45</td>
      <td>46</td>
      <td>47</td>
    </tr>
    <tr>
      <th>8</th>
      <td>64</td>
      <td>65</td>
      <td>66</td>
      <td>67</td>
      <td>68</td>
      <td>69</td>
      <td>70</td>
      <td>71</td>
    </tr>
    <tr>
      <th>9</th>
      <td>72</td>
      <td>73</td>
      <td>74</td>
      <td>75</td>
      <td>76</td>
      <td>77</td>
      <td>78</td>
      <td>79</td>
    </tr>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
      <td>4</td>
      <td>5</td>
      <td>6</td>
      <td>7</td>
    </tr>
    <tr>
      <th>6</th>
      <td>48</td>
      <td>49</td>
      <td>50</td>
      <td>51</td>
      <td>52</td>
      <td>53</td>
      <td>54</td>
      <td>55</td>
    </tr>
    <tr>
      <th>4</th>
      <td>32</td>
      <td>33</td>
      <td>34</td>
      <td>35</td>
      <td>36</td>
      <td>37</td>
      <td>38</td>
      <td>39</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-dc43912a-3894-422d-a00e-5c0d59efce06')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-dc43912a-3894-422d-a00e-5c0d59efce06 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-dc43912a-3894-422d-a00e-5c0d59efce06');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```
# Random sample without replacement

df.take(np.random.permutation(len(df))[:3])
```





  <div id="df-01fe0b5d-eb7a-4a02-8e6e-4392c3ecc2dc">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>6</th>
      <td>48</td>
      <td>49</td>
      <td>50</td>
      <td>51</td>
      <td>52</td>
      <td>53</td>
      <td>54</td>
      <td>55</td>
    </tr>
    <tr>
      <th>2</th>
      <td>16</td>
      <td>17</td>
      <td>18</td>
      <td>19</td>
      <td>20</td>
      <td>21</td>
      <td>22</td>
      <td>23</td>
    </tr>
    <tr>
      <th>3</th>
      <td>24</td>
      <td>25</td>
      <td>26</td>
      <td>27</td>
      <td>28</td>
      <td>29</td>
      <td>30</td>
      <td>31</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-01fe0b5d-eb7a-4a02-8e6e-4392c3ecc2dc')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-01fe0b5d-eb7a-4a02-8e6e-4392c3ecc2dc button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-01fe0b5d-eb7a-4a02-8e6e-4392c3ecc2dc');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```
# Random sample with replacement
sack = np.array([4, 8, -2, 7, 5])
sampler = np.random.randint(0, len(sack), size = 10)
sampler
```




    array([2, 3, 4, 4, 1, 2, 1, 1, 2, 4])



##2.8.1 Exercise


```
"""
Exercise: Draw numbers from sack using sampler
"""

"""
Solution
draw = sack.take(sampler)
draw 
"""

```




    array([-2,  7,  5,  5,  8, -2,  8,  8, -2,  5])



## 2.8.2 Exercise


```
'''
Exercise : 
Create a random numpy array with integers between -10 and 10 containing 5 integers.
Find out the standard deviation of the array.

Solution :
import numpy as np
arr = np.random.randint(-10,10,size=5)
arr
import pandas as pd
arr_df = pd.DataFrame(arr)
arr_df.describe()

'''
```




    array([-1, -7,  4, -8, -4])



## 2.8.3 Exercise


```
'''
Exercise :
Create a random numpy array containing 9 integers and reshape it into a 3*3 array.
Replace the integers in the 2nd row with random negative integers.

Solution :
arr = np.arange(9).reshape((3, 3))
array = np.random.permutation(arr)
array
for i in range (0,3):
  array[1][i]= np.random.randint(-5,-2)
array
'''
```




    '\nExercise :\nCreate a random numpy array containing 9 integers and reshape it into a 3*3 array.\nReplace the integers in the 2nd row with random negative integers.\n\nSolution :\narr = np.arange(9).reshape((3, 3))\narray = np.random.permutation(arr)\narray\nfor i in range (0,3):\n  array[1][i]= np.random.randint(-5,-2)\narray\n'



## 2.8.4 Exercise


```
'''
Exercise :
Generate a uniform random sample from np.arange(5) of size 3 without replacement:
(a) using choice
(b) using permutation

Solution :
np.random.choice(5, 3, replace=False)
np.random.permutation(np.arange(5))[:3]
'''

```




    7.13241232488206



## 2.8.5 Exercise


```
'''
Exercise : 
(a) Generate a 2 x 4 array of ints between 0 and 4, inclusive:
(b) Generate a 1 by 3 array with 3 different lower bounds
(c) Generate a 1 x 3 array with 3 different upper bound

Solution :
rng = np.random.default_rng()
rng.integers(5, size=(2, 4))
rng.integers([1, 5, 7], 10)
rng.integers(1, [3, 5, 10])
'''
```

#2.9 Dummy variables


```
df = pd.DataFrame({'gender': ['female', 'female', 'male', 'unknown', 'male', 'female'], 'votes': range(6, 12, 1)})
df
```





  <div id="df-60009b63-5f95-4e9f-b677-2e0523cd1921">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>gender</th>
      <th>votes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>female</td>
      <td>6</td>
    </tr>
    <tr>
      <th>1</th>
      <td>female</td>
      <td>7</td>
    </tr>
    <tr>
      <th>2</th>
      <td>male</td>
      <td>8</td>
    </tr>
    <tr>
      <th>3</th>
      <td>unknown</td>
      <td>9</td>
    </tr>
    <tr>
      <th>4</th>
      <td>male</td>
      <td>10</td>
    </tr>
    <tr>
      <th>5</th>
      <td>female</td>
      <td>11</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-60009b63-5f95-4e9f-b677-2e0523cd1921')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-60009b63-5f95-4e9f-b677-2e0523cd1921 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-60009b63-5f95-4e9f-b677-2e0523cd1921');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```
pd.get_dummies(df['gender'])
```





  <div id="df-ed482da7-e2c7-40ec-ac3c-f10f4c1c88db">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>female</th>
      <th>male</th>
      <th>unknown</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-ed482da7-e2c7-40ec-ac3c-f10f4c1c88db')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-ed482da7-e2c7-40ec-ac3c-f10f4c1c88db button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-ed482da7-e2c7-40ec-ac3c-f10f4c1c88db');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```
dummies = pd.get_dummies(df['gender'], prefix='gender')
dummies
```





  <div id="df-1f96ff4c-03b3-4498-8a20-d9a9c43d6361">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>gender_female</th>
      <th>gender_male</th>
      <th>gender_unknown</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-1f96ff4c-03b3-4498-8a20-d9a9c43d6361')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-1f96ff4c-03b3-4498-8a20-d9a9c43d6361 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-1f96ff4c-03b3-4498-8a20-d9a9c43d6361');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




##2.9.1 Exercise 


```
"""
Exercise Join votes column with dummies dataframe
"""

"""
Solution
with_dummy = df[['votes']].join(dummies)
with_dummy
"""

```





  <div id="df-ddffabbd-9a3e-4545-a664-77ecbdfa7696">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>votes</th>
      <th>gender_female</th>
      <th>gender_male</th>
      <th>gender_unknown</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>6</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>7</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>8</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>9</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>10</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>11</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-ddffabbd-9a3e-4545-a664-77ecbdfa7696')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-ddffabbd-9a3e-4545-a664-77ecbdfa7696 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-ddffabbd-9a3e-4545-a664-77ecbdfa7696');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




##  2.9.2 Exercise

Create a dataframe consisting of the following data and Get the Dummy variables from the dataframe:

ids = [11, 22, 33, 44, 55, 66, 77]
countries = ['Spain', 'France', 'Spain', 'Germany', 'France']


```
import pandas as pd

ids = [11, 22, 33, 44, 55, 66, 77]
countries = ['Spain', 'France', 'Spain', 'Germany', 'France']

df = pd.DataFrame(list(zip(ids, countries)),
                  columns=['Ids', 'Countries'])
```


```
y = pd.get_dummies(df.Countries, prefix='Country')
print(y.head())
```

       Country_France  Country_Germany  Country_Spain
    0               0                0              1
    1               1                0              0
    2               0                0              1
    3               0                1              0
    4               1                0              0


##2.9.3 Exercise

Get Dummy Variables from following data


df = pd.DataFrame({
  
    'A': ['hello', 'vignan', 'geeks'],
                   
                   
    'B': ['vignan', 'hello', 'hello'],
  
  
    'C': [1, 2, 3]
  })


```
"""
Solution
"""
import pandas as pd
import numpy as np
 
# create dataset
df = pd.DataFrame({'A': ['hello', 'vignan', 'geeks'],
                   'B': ['vignan', 'hello', 'hello'],
                   'C': [1, 2, 3]})
 
# display dataset
print(df)
 
# create dummy variables
pd.get_dummies(df)
```

            A       B  C
    0   hello  vignan  1
    1  vignan   hello  2
    2   geeks   hello  3






  <div id="df-1f1e0701-ffe1-4a72-a3aa-6e61c8cd7b41">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>C</th>
      <th>A_geeks</th>
      <th>A_hello</th>
      <th>A_vignan</th>
      <th>B_hello</th>
      <th>B_vignan</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-1f1e0701-ffe1-4a72-a3aa-6e61c8cd7b41')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-1f1e0701-ffe1-4a72-a3aa-6e61c8cd7b41 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-1f1e0701-ffe1-4a72-a3aa-6e61c8cd7b41');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




## 2.9.4 Exercise

(a) Find the number of unique values in the location column of the following dataset. [Dataset](https://drive.google.com/file/d/1FyYE1_hbmn5L0TX80B6cKT0UljC_-YAd/view?usp=sharing)




```
'''
import opendatasets as od
link = "https://drive.google.com/file/d/1FyYE1_hbmn5L0TX80B6cKT0UljC_-YAd/view?usp=sharing"
dataframe = od.download(link)
train_inputs.Location.unique()
'''
```

## 2.9.5 Exercise

(b) Carry out One-Hot encoding using scikit learn on the cities column of this dataset. [Dataset](https://drive.google.com/file/d/1FyYE1_hbmn5L0TX80B6cKT0UljC_-YAd/view?usp=sharing)


```
'''
import opendatasets as od
link = "https://drive.google.com/file/d/1FyYE1_hbmn5L0TX80B6cKT0UljC_-YAd/view?usp=sharing"
dataframe = od.download(link)


from sklearn.preprocessing import OneHotEncoder

categorical_cols = dataframe.select_dtypes('object').columns.tolist()
encoder = OneHotEncoder(sparse=False, handle_unknown='ignore').fit(dataframe[categorical_cols])
'''
```




    '\nimport opendatasets as od\nlink = "https://drive.google.com/file/d/1FyYE1_hbmn5L0TX80B6cKT0UljC_-YAd/view?usp=sharing"\ndataframe = od.download(link)\n\n\nfrom sklearn.preprocessing import OneHotEncoder\n\ncategorical_cols = dataframe.select_dtypes(\'object\').columns.tolist()\nencoder = OneHotEncoder(sparse=False, handle_unknown=\'ignore\').fit(dataframe[categorical_cols])\n'


