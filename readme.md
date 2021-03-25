Fast add Category in breadcrumbs on Product page
=========

* Open catalog/controller/product/product.php

Search : 
```
$this->load->model('catalog/product');
```

cut it and place after 

```
$this->load->model('catalog/category');
$this->load->model('catalog/product');
```

Found this :

```
if (isset($this->request->get['path'])) {
...
...
}
```

after closing brace add

```
} else {
    if(isset($this->request->get['product_id'])) {

        $getCategories = $this->model_catalog_product->getCategories($this->request->get['product_id']);
        $category = array_shift($getCategories);
        $category_info = $this->model_catalog_category->getCategory($category['category_id']);

        if ($category_info) {
            $url = '';

            if (isset($this->request->get['sort'])) {
                $url .= '&sort=' . $this->request->get['sort'];
            }

            if (isset($this->request->get['order'])) {
                $url .= '&order=' . $this->request->get['order'];
            }

            if (isset($this->request->get['page'])) {
                $url .= '&page=' . $this->request->get['page'];
            }

            if (isset($this->request->get['limit'])) {
                $url .= '&limit=' . $this->request->get['limit'];
            }

            $data['breadcrumbs'][] = array(
                'text' => $category_info['name'],
                'href' => $this->url->link('product/category', 'path=' . $category['category_id'] . $url)
            );
        }
    }
}

```

Best regards [Moris Finkel](mailto:moris@moris-web.com)

[Moris-Web](http://moris-web.com)

