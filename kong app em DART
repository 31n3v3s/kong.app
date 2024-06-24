import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Kong Store',
      theme: ThemeData(
        primarySwatch: Colors.brown,
      ),
      initialRoute: '/',
      routes: {
        '/': (context) => HomeScreen(),
        '/login': (context) => LoginScreen(),
        '/signup': (context) => SignupScreen(),
      },
    );
  }
}

class HomeScreen extends StatefulWidget {
  @override
  _HomeScreenState createState() => _HomeScreenState();
}

class _HomeScreenState extends State<HomeScreen> {
  final List<Product> _products = [
    Product(
      id: 'p1',
      title: 'Camiseta',
      description: 'Uma camiseta legal',
      price: 29.99,
      imageUrl:
          'https://static.vecteezy.com/system/resources/previews/024/029/733/non_2x/gorilla-black-and-white-clipart-transparent-background-free-png.png',
      sizes: ['P', 'M', 'G', 'GG'],
    ),
    Product(
      id: 'p2',
      title: 'Camiseta Estampada',
      description: 'Camiseta estampada legal',
      price: 34.99,
      imageUrl: 'https://example.com/images/graphic-tee.jpg',
      sizes: ['P', 'M', 'G', 'GG'],
    ),
    Product(
      id: 'p3',
      title: 'Camisa Polo',
      description: 'Camisa polo clássica',
      price: 39.99,
      imageUrl: 'https://example.com/images/polo-shirt.jpg',
      sizes: ['P', 'M', 'G', 'GG'],
    ),
    Product(
      id: 'p4',
      title: 'Bermuda Cargo',
      description: 'Bermuda cargo com bolsos',
      price: 49.99,
      imageUrl: 'https://example.com/images/cargo-shorts.jpg',
      sizes: ['38', '40', '42', '44'],
    ),
    Product(
      id: 'p5',
      title: 'Bermuda Jeans',
      description: 'Bermuda jeans para uso casual',
      price: 39.99,
      imageUrl: 'https://example.com/images/denim-shorts.jpg',
      sizes: ['38', '40', '42', '44'],
    ),
    Product(
      id: 'p6',
      title: 'Bermuda Chino',
      description: 'Bermuda chino em várias cores',
      price: 44.99,
      imageUrl: 'https://example.com/images/chino-shorts.jpg',
      sizes: ['38', '40', '42', '44'],
    ),
  ];

  final List<CartItem> _cartItems = [];
  final List<Product> _favoriteProducts = [];

  void _addToCart(Product product, int quantity, String size) {
    setState(() {
      _cartItems
          .add(CartItem(product: product, quantity: quantity, size: size));
    });
  }

  void _removeFromCart(int index) {
    setState(() {
      _cartItems.removeAt(index);
    });
  }

  void _toggleFavorite(Product product) {
    setState(() {
      if (_favoriteProducts.contains(product)) {
        _favoriteProducts.remove(product);
      } else {
        _favoriteProducts.add(product);
      }
    });
  }

  bool _isFavorite(Product product) {
    return _favoriteProducts.contains(product);
  }

  void _checkout() {
    setState(() {
      _cartItems.clear();
    });
    showDialog(
      context: context,
      builder: (ctx) => AlertDialog(
        title: Text('Compra Finalizada'),
        content: Text('Obrigado por sua compra!'),
        actions: <Widget>[
          TextButton(
            child: Text('OK'),
            onPressed: () {
              Navigator.of(ctx).pop();
            },
          )
        ],
      ),
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Kong Store'),
      ),
      body: Stack(
        children: [
          Image.network(
            'https://static.vecteezy.com/system/resources/previews/024/029/733/non_2x/gorilla-black-and-white-clipart-transparent-background-free-png.png',
            fit: BoxFit.cover,
            width: double.infinity,
            height: double.infinity,
          ),
          ProductGrid(
            products: _products,
            addToCart: _addToCart,
            toggleFavorite: _toggleFavorite,
            isFavorite: _isFavorite,
          ),
        ],
      ),
      bottomNavigationBar: BottomNavigationBar(
        items: [
          BottomNavigationBarItem(
            icon: Icon(Icons.home),
            label: 'Home',
          ),
          BottomNavigationBarItem(
            icon: Icon(Icons.shopping_cart),
            label: 'Carrinho',
          ),
          BottomNavigationBarItem(
            icon: Icon(Icons.person),
            label: 'Login',
          ),
        ],
        onTap: (index) {
          if (index == 1) {
            Navigator.of(context).push(
              MaterialPageRoute(
                builder: (ctx) => CartScreen(
                  cartItems: _cartItems,
                  removeFromCart: _removeFromCart,
                  checkout: _checkout,
                ),
              ),
            );
          } else if (index == 2) {
            Navigator.of(context).pushNamed('/login');
          }
        },
      ),
    );
  }
}

class Product {
  final String id;
  final String title;
  final String description;
  final double price;
  final String imageUrl;
  final List<String> sizes;

  Product({
    required this.id,
    required this.title,
    required this.description,
    required this.price,
    required this.imageUrl,
    required this.sizes,
  });
}

class ProductGrid extends StatelessWidget {
  final List<Product> products;
  final Function(Product, int, String) addToCart;
  final Function(Product) toggleFavorite;
  final Function(Product) isFavorite;

  ProductGrid({
    required this.products,
    required this.addToCart,
    required this.toggleFavorite,
    required this.isFavorite,
  });

  @override
  Widget build(BuildContext context) {
    return GridView.builder(
      padding: const EdgeInsets.all(10.0),
      itemCount: products.length,
      itemBuilder: (ctx, i) => ProductItem(
        product: products[i],
        addToCart: addToCart,
        toggleFavorite: toggleFavorite,
        isFavorite: isFavorite,
      ),
      gridDelegate: SliverGridDelegateWithFixedCrossAxisCount(
        crossAxisCount: 2,
        childAspectRatio: 3 / 2,
        crossAxisSpacing: 10,
        mainAxisSpacing: 10,
      ),
    );
  }
}

class ProductItem extends StatelessWidget {
  final Product product;
  final Function(Product, int, String) addToCart;
  final Function(Product) toggleFavorite;
  final Function(Product) isFavorite;

  ProductItem({
    required this.product,
    required this.addToCart,
    required this.toggleFavorite,
    required this.isFavorite,
  });

  @override
  Widget build(BuildContext context) {
    return InkWell(
      onTap: () {
        _showSizeAndQuantityDialog(context, product);
      },
      child: Card(
        elevation: 5,
        shape: RoundedRectangleBorder(
          borderRadius: BorderRadius.circular(15),
        ),
        child: Column(
          children: [
            Stack(
              children: [
                Hero(
                  tag: product.id,
                  child: FadeInImage(
                    placeholder: AssetImage('assets/images/placeholder.png'),
                    image: NetworkImage(product.imageUrl),
                    fit: BoxFit.cover,
                  ),
                ),
                Positioned(
                  top: 8,
                  right: 8,
                  child: IconButton(
                    icon: Icon(
                      isFavorite(product)
                          ? Icons.favorite
                          : Icons.favorite_border,
                      color: Colors.red,
                    ),
                    onPressed: () {
                      toggleFavorite(product);
                    },
                  ),
                ),
              ],
            ),
            Padding(
              padding: const EdgeInsets.all(10.0),
              child: Text(
                product.title,
                style: TextStyle(fontSize: 16, fontWeight: FontWeight.bold),
                textAlign: TextAlign.center,
              ),
            ),
            Padding(
              padding: const EdgeInsets.all(10.0),
              child: Text(
                'R\$${product.price.toStringAsFixed(2)}',
                style: TextStyle(fontSize: 16, color: Colors.grey),
              ),
            ),
          ],
        ),
      ),
    );
  }

  void _showSizeAndQuantityDialog(BuildContext context, Product product) {
    int quantity = 1;
    String selectedSize = product.sizes[0];

    showDialog(
      context: context,
      builder: (ctx) {
        return AlertDialog(
          title: Text('Selecionar Tamanho e Quantidade'),
          content: Column(
            mainAxisSize: MainAxisSize.min,
            children: [
              DropdownButton<String>(
                value: selectedSize,
                onChanged: (newValue) {
                  selectedSize = newValue!;
                },
                items: product.sizes.map((size) {
                  return DropdownMenuItem(
                    child: Text(size),
                    value: size,
                  );
                }).toList(),
              ),
              TextField(
                decoration: InputDecoration(labelText: 'Quantidade'),
                keyboardType: TextInputType.number,
                onChanged: (value) {
                  quantity = int.parse(value);
                },
              ),
            ],
          ),
          actions: [
            TextButton(
              child: Text('Cancelar'),
              onPressed: () {
                Navigator.of(ctx).pop();
              },
            ),
            ElevatedButton(
              child: Text('Adicionar ao Carrinho'),
              onPressed: () {
                addToCart(product, quantity, selectedSize);
                Navigator.of(ctx).pop();
              },
            ),
          ],
        );
      },
    );
  }
}

class CartItem {
  final Product product;
  final int quantity;
  final String size;

  CartItem({
    required this.product,
    required this.quantity,
    required this.size,
  });
}

class CartScreen extends StatelessWidget {
  final List<CartItem> cartItems;
  final Function(int) removeFromCart;
  final Function checkout;

  CartScreen({
    required this.cartItems,
    required this.removeFromCart,
    required this.checkout,
  });

  @override
  Widget build(BuildContext context) {
    double total = 0;
    cartItems.forEach((cartItem) {
      total += cartItem.product.price * cartItem.quantity;
    });

    return Scaffold(
      appBar: AppBar(
        title: Text('Carrinho de Compras'),
      ),
      body: Column(
        children: [
          Expanded(
            child: ListView.builder(
              itemCount: cartItems.length,
              itemBuilder: (ctx, i) => ListTile(
                leading: CircleAvatar(
                  backgroundImage: NetworkImage(cartItems[i].product.imageUrl),
                ),
                title: Text(cartItems[i].product.title),
                subtitle: Text(
                    'Tamanho: ${cartItems[i].size}\nQuantidade: ${cartItems[i].quantity}'),
                trailing: IconButton(
                  icon: Icon(Icons.delete),
                  onPressed: () => removeFromCart(i),
                ),
              ),
            ),
          ),
          Padding(
            padding: const EdgeInsets.all(8.0),
            child: Text(
              'Total: R\$${total.toStringAsFixed(2)}',
              style: TextStyle(fontSize: 20, fontWeight: FontWeight.bold),
            ),
          ),
          SizedBox(height: 10),
          ElevatedButton(
            onPressed: () => checkout(),
            child: Text('Finalizar Compra'),
          ),
        ],
      ),
    );
  }
}

class LoginScreen extends StatelessWidget {
  final TextEditingController _emailController = TextEditingController();
  final TextEditingController _passwordController = TextEditingController();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Login'),
      ),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            TextField(
              controller: _emailController,
              decoration: InputDecoration(labelText: 'Email'),
            ),
            TextField(
              controller: _passwordController,
              decoration: InputDecoration(labelText: 'Senha'),
              obscureText: true,
            ),
            SizedBox(height: 20),
            ElevatedButton(
              child: Text('Login'),
              onPressed: () {
                // Implement login functionality here
                Navigator.of(context).pushReplacementNamed('/');
              },
            ),
            TextButton(
              child: Text('Não tem uma conta? Registre-se'),
              onPressed: () {
                Navigator.of(context).pushReplacementNamed('/signup');
              },
            ),
          ],
        ),
      ),
    );
  }
}

class SignupScreen extends StatelessWidget {
  final TextEditingController _emailController = TextEditingController();
  final TextEditingController _passwordController = TextEditingController();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Registrar-se'),
      ),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            TextField(
              controller: _emailController,
              decoration: InputDecoration(labelText: 'Email'),
            ),
            TextField(
              controller: _passwordController,
              decoration: InputDecoration(labelText: 'Senha'),
              obscureText: true,
            ),
            SizedBox(height: 20),
            ElevatedButton(
              child: Text('Registrar'),
              onPressed: () {
                // Implement signup functionality here
                Navigator.of(context).pushReplacementNamed('/');
              },
            ),
            TextButton(
              child: Text('Já tem uma conta? Faça login'),
              onPressed: () {
                Navigator.of(context).pushReplacementNamed('/login');
              },
            ),
          ],
        ),
      ),
    );
  }
}
