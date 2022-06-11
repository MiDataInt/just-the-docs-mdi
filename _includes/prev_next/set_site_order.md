{%- assign site_order = 999999 -%}
{%- if query_page.grand_parent -%}
    {%- for parent in site.pages -%}
        {%- if parent.title == query_page.parent -%}
            {%- assign parent_order = parent.nav_order | times: 100 -%}
            {%- for grandparent in site.pages -%}
                {%- if grandparent.title == parent.parent -%}
                    {%- assign site_order = grandparent.nav_order | times: 10000 | plus: parent_order | plus: query_page.nav_order -%}
                {%- endif -%}
            {%- endfor -%}
        {%- endif -%}
    {%- endfor -%}
{%- elsif query_page.parent -%}
    {%- assign page_order = query_page.nav_order | times: 100 -%}
    {%- for parent in site.pages -%}
        {%- if parent.title == query_page.parent -%}
            {%- assign site_order = parent.nav_order | times: 10000 | plus: page_order -%}
        {%- endif -%}
    {%- endfor -%}
{%- else -%}
    {%- assign site_order = query_page.nav_order | times: 10000 -%}
{%- endif -%}