## Welcome to Forex_Vantage

In this section I will use Alpha Vantage API to analyze forex data. Let's first import some required libraries. To use any API we are generally required to pass an API key with the search parameters. So, for AlphaVantageAPI we can get one from https://www.alphavantage.co/. In this approach I'll rather use a library by RomellTorres to explore the AlphaVantageAPI, and not the API site.
Let's begin.

```
import pandas as pd        #for dataframe visualization
from alpha_vantage.foreignexchange import ForeignExchange as FX    #library to use AlphaVantageAPI without link requests
```

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/Irfan-Ahmad-byte/Forex_Vantage/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
