# logger_apply

## Documentation
The documentation is hosted at [https://github.com/BingerYang/logger_apply](https://github.com/BingerYang/logger_apply)

## Installation
```shell
 pip install logger_apply
```
## Usage

```python
# -*- coding: utf-8 -*- 

from logger_app import FormatterRule, LoggerApply
from flask import request, Flask

app = Flask(__name__)
app.config['PROPAGATE_EXCEPTIONS'] = False  # 设置是否传递异常 , 如果为True, 则flask运行中的错误会显示到网页中, 如果为False, 则会输出到文件中


# FormatterRule.CB_TAG_MAP = dict(path=lambda: request.path, md5=lambda: request.host_url)


@app.route('/')
def index():
    # num = 1 / 0
    app.logger.error('this is a error')
    return "index"


if __name__ == '__main__':
    app.logger = LoggerApply(__name__, fmt=FormatterRule(style='json')).create_logger()

    app.run(debug=True)

```