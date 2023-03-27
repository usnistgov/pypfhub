---
jupyter:
  jupytext:
    formats: ipynb,md
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.3'
      jupytext_version: 1.14.2-dev
  kernelspec:
    display_name: Python 3 (ipykernel)
    language: python
    name: python3
---

```python papermill={"duration": 0.01592, "end_time": "2023-03-15T16:01:51.917192", "exception": false, "start_time": "2023-03-15T16:01:51.901272", "status": "completed"} tags=["parameters"]
benchmark_id = '3a.1'
line_plots = [
    dict(name='free_energy', layout=dict(log_y=True, x_label=r'<i>t</i>', y_label=r'&#8497;', range_y=[1.8e6, 2.4e6], title="Free Energy v Time")),
    dict(name='solid_fraction', layout=dict(log_y=True, x_label=r'<i>t</i>')),
    dict(name='tip_position', layout=dict(log_y=True, x_label=r'<i>t</i>')),
    dict(name='phase_field_1500', layout=dict(aspect_ratio=1.0))
]
contour_plots = []
```

```python papermill={"duration": 0.009772, "end_time": "2023-03-15T16:01:51.932513", "exception": false, "start_time": "2023-03-15T16:01:51.922741", "status": "completed"} tags=["injected-parameters"]
# Parameters
benchmark_id = "2d.1"
line_plots = [
    {
        "name": "free_energy",
        "layout": {
            "log_y": True,
            "log_x": True,
            "x_label": "Simulated Time, <i>t</i><sub>Sim</sub>&nbsp;[a.u.]",
            "y_label": "Simulated Free Energy, &#8497;&nbsp;[a.u.]",
            "title": "",
        },
    }
]

```

```python papermill={"duration": 0.011478, "end_time": "2023-03-15T16:01:51.946431", "exception": false, "start_time": "2023-03-15T16:01:51.934953", "status": "completed"} tags=[]
from IPython.display import display_markdown

display_markdown(f'''
# Benchmark { benchmark_id } Results

All results for the [{ benchmark_id } benchmark specification](../../benchmarks/benchmark{ benchmark_id }.ipynb/).
''', raw=True)
```

```python papermill={"duration": 0.009891, "end_time": "2023-03-15T16:01:51.958709", "exception": false, "start_time": "2023-03-15T16:01:51.948818", "status": "completed"} tags=[]
# To generate the comparison notebooks use:
# 
# papermill template.ipynb benchmark{version}.ipynb -f bm{version}.yaml
#
```

```python papermill={"duration": 0.015863, "end_time": "2023-03-15T16:01:51.977228", "exception": false, "start_time": "2023-03-15T16:01:51.961365", "status": "completed"} tags=[]
from IPython.display import HTML

HTML('''<script>
code_show=true; 
function code_toggle() {
 if (code_show){
 $('div.input').hide();
 $('div.prompt').hide();
 } else {
 $('div.input').show();
$('div.prompt').show();
 }
 code_show = !code_show
} 
$( document ).ready(code_toggle);
</script>
<form action="javascript:code_toggle()"><input type="submit" value="Code Toggle"></form>''')
```

```python papermill={"duration": 0.709019, "end_time": "2023-03-15T16:01:52.690851", "exception": false, "start_time": "2023-03-15T16:01:51.981832", "status": "completed"} tags=[]
#from IPython.display import HTML, display
#from time import sleep

#display(HTML("""
#<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/2.1.1/jquery.min.js"></script>
#"""))

#sleep(0.1)

from IPython.display import HTML, display, display_markdown
from time import sleep

#import logging
#logging.basicConfig(format='%(asctime)s - %(message)s', level=logging.DEBUG)

display(HTML("""
<script src="https://cdnjs.cloudflare.com/ajax/libs/require.js/2.1.10/require.min.js"></script>
"""))

sleep(0.1)


from pfhub.main import line_plot, levelset_plot, get_table_data_style, plot_order_of_accuracy, get_result_data, efficiency_plot
#import itables.interactive
from itables import init_notebook_mode

init_notebook_mode(all_interactive=False)
```

```python papermill={"duration": 3.85348, "end_time": "2023-03-15T16:01:56.546898", "exception": false, "start_time": "2023-03-15T16:01:52.693418", "status": "completed"} tags=[]
for x in line_plots:
    line_plot(
        data_name=x['name'],
        benchmark_id=benchmark_id,
        layout=x['layout'],
        columns=x.get('columns', ('x', 'y'))
    ).show()
```

```python papermill={"duration": 0.132655, "end_time": "2023-03-15T16:01:56.812163", "exception": false, "start_time": "2023-03-15T16:01:56.679508", "status": "completed"} tags=[]
for x in contour_plots:
    data = get_result_data([x['name']], [benchmark_id], x['columns'])

    levelset_plot(
        data,
        layout=x['layout'],
        mask_func=lambda df: (x['mask_z'][0] < df.z) & (df.z < x['mask_z'][1]),
        columns=x['columns']
    ).show()
```

```python papermill={"duration": 2.440714, "end_time": "2023-03-15T16:01:59.390859", "exception": false, "start_time": "2023-03-15T16:01:56.950145", "status": "completed"} tags=[]
efficiency_plot(benchmark_id).show()

display_markdown("<span class='plotly-footnote' >* Wall time divided by the total simulated time.</span>", raw=True)

```

```python papermill={"duration": 0.123466, "end_time": "2023-03-15T16:01:59.637213", "exception": false, "start_time": "2023-03-15T16:01:59.513747", "status": "completed"} tags=[]
display_markdown(f'''
# Table of Results

Table of { benchmark_id } benchmark result uploads.
''', raw=True)
```

```python papermill={"duration": 0.113281, "end_time": "2023-03-15T16:01:59.861104", "exception": false, "start_time": "2023-03-15T16:01:59.747823", "status": "completed"} tags=[]

```

```python papermill={"duration": 1.357501, "end_time": "2023-03-15T16:02:01.340707", "exception": false, "start_time": "2023-03-15T16:01:59.983206", "status": "completed"} tags=[]
## Currently switching off interactive tables as these are not converted to HTML properly.
## This might improve when jupyter-nbcovert is updated to a later version.

init_notebook_mode(all_interactive=False)
get_table_data_style(benchmark_id, pfhub_path='../..')
```

```python papermill={"duration": 0.135636, "end_time": "2023-03-15T16:02:01.636347", "exception": false, "start_time": "2023-03-15T16:02:01.500711", "status": "completed"} tags=[]

```