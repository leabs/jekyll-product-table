# jekyll-product-catalog

This [Jekyll](https://jekyllrb.com/) site uses Jekyll collections to iterate over markdown file frontmatter and populates those properties into a sortable searchable table using the DataTables plug-in. This is a good set up for a light weight store of information for items such as parts with specs. It is a static site, so loading thousands of parts is as fast as possible, secure since there is no back end, and can be organized as the owner sees fit using the `_skus` folder as the repository for parts data. It also uses [bulma css framework](https://bulma.io/) for some basic styling (container, typography, table).

### Requirements

To build and run this site locally, you will need

- [Ruby](https://www.ruby-lang.org/en/)
- [Bundler](https://bundler.io/)
- [Jekyll](https://jekyllrb.com/)

### Install Locally

- Download, clone, or fork the repository.
- Navigate to the repository directory.
- Run `bundle install` in the repository directory.
- Run `bundle exec jekyll serve`.
- Open [http://127.0.0.1:4000/](http://127.0.0.1:4000/).

### Deploy

There are many options for deploying Jekyll sites. My current favorite option is [Vercel](https://vercel.com/) which can build and host your site. You can additionally set up domains in their dashboard.

Other options include:

- GitHub pages
- AWS S3
- Netlify
- GitLab pages

More info on deployment methods (including automated options) can be found [here.](https://jekyllrb.com/docs/deployment/)

### Adding additional parts

Add parts into the `_skus` directory, using the exisiting parts as a guide. Any of the information within these markdown files can be pulled into the DataTable.

### Adding additional properties

Adding any new property to the sku's frontmatter requires the addition of the `{{sku.propName}}` to the **tbody** as well as the **thead** found at `_layouts/home.html`.

Here is what the FOR loop looks like using Jekyll's Liquid engine:

```
<tbody>
    <!--For loop that iterates over markdown frontmatter in _skus folder-->
    {% for sku in site.skus %}
        <tr>
            <td>{{ sku.Name }}</td>
            <td>{{ sku.Sku }}</td>
            <td>{{ sku.Price }}</td>
            <td>{{ sku.content | markdownify }}</td>
        </tr>
    {% endfor %}
</tbody>
```

### Additional options

Site title, description, and more can be edited in the `_config.yml` file. Any changes to this file will require a server reboot if you are building locally.

### Sorting the table

By default the table sorts by Sku number. To change sorting, go to `_layouts/home.html` line 717 and adjust `order: [[1, "asc"]],` to your liking.
