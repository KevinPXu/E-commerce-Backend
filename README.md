# E-commerce-Backend

## Technologies Used

- JavaScript
- Node.js
- express.js
- nodemon.js
- mysql + mysql express package
- dotenv
- sequelize
- console.table
- VS Code
- Git
- GitHub

## Summary

This project was used to obtain a better understanding of using an ORM and querying for data using a backend server through express. We were able to create a database and query it using express routes that called certain URL endpoints. Through these endpoints, we used CRUD operations to get, update, create and delete entries from the databases and their referenced tables.

## Demonstration

View demo: https://drive.google.com/file/d/1s68vg5QQRCabLtSBCo2mV6fFOPTnAL7N/view

## Description

A E-Commerce backend with numerous API endpoints to Get, Create, Update, and Delete Data. When using the Get routes, you can retrieve all the data from a given table including all the referenced tables included. If you specify which ID you want to get, it will retrieve a single entry in that table. If you update, it will update depending on the ID you gave it. If you delete, it will delete the entry id you gave it in the endpoint. If you create, it will create a new entry in the table you specify.

## Code Snippet

### Relationships between the tables created

```JavaScript
ProductTag.init(
  {
    id: {
      type: DataTypes.INTEGER,
      allowNull: false,
      primaryKey: true,
      autoIncrement: true,
    },
    product_id: {
      type: DataTypes.INTEGER,
      references: {
        model: "product",
        key: "id",
      },
      onDelete: "CASCADE",
    },
    tag_id: {
      type: DataTypes.INTEGER,
      references: {
        model: "tag",
        key: "id",
      },
      onDelete: "CASCADE",
    },
  },
  {
    sequelize,
    timestamps: false,
    freezeTableName: true,
    underscored: true,
    modelName: "product_tag",
  }
);
```

### example of a get request

```JavaScript
router.get("/", async (req, res) => {
  // find all categories
  // be sure to include its associated Products
  try {
    const categoryData = await Category.findAll({
      include: [{ model: Product }],
    });
    res.status(200).json(categoryData);
  } catch (err) {
    res.status(500).json(err);
  }
});
```

### example of a put request (Note\* put and delete are very similar operations)

```JavaScript
router.put("/:id", async (req, res) => {
  // update a category by its `id` value
  try {
    const categoryData = await Category.update(
      { category_name: req.body.category_name },
      {
        where: {
          id: req.params.id,
        },
      }
    );

    if (!categoryData) {
      res.status(404).json({ message: "No category with that ID found" });
      return;
    }
    res.status(204);
  } catch (err) {
    res.status(500).json(err);
  }
});

```

### example of a create request

```JavaScript
router.post("/", async (req, res) => {
  // create a new category
  try {
    const categoryData = await Category.create({
      category_name: req.body.category_name,
    });
    res.status(201).json(categoryData);
  } catch (err) {
    res.status(400).json(err);
  }
});

```

## Author Links

[LinkedIn](https://www.linkedin.com/in/kevin-xu-4672a7215/)
[GitHub](https://github.com/KevinPXu)
1
