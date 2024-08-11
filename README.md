# Image Product Search

Image Product Search is a powerful tool that enables searching for products using either text descriptions or example images. It leverages advanced AI models to understand and index product images, allowing for efficient and accurate retrieval of similar products.

## Features

- Asynchronous downloading of product images
- Image embedding generation using Facebook's ImageBind model
- Efficient indexing and searching with DocArray and HNSW
- Multimodal search capabilities (text and image)
- Support for both CPU and GPU processing

## Prerequisites

- Python 3.7+
- PyTorch
- torchvision
- ImageBind
- DocArray
- pandas
- aiohttp
- aiofiles
- Other dependencies (see `requirements.txt`)

## Installation

1. Clone this repository:
   ```
   git clone https://github.com/Balogunolalere/image-product-search.git
   cd image-product-search
   ```

2. Install the required packages:
   ```
   pip install -r requirements.txt
   ```


## Usage

1. Prepare your product data in JSON format (see `jendol.json` for example structure).

2. Set the path to your JSON file:
   ```python
   data = pd.read_json('/path/to/your/product_data.json')
   ```

3. Run the main script:
   ```
   python image_product_search.py
   ```

4. The script will download images, generate embeddings, and index them.

5. Use the `find` method to search for products:
   ```python
   # Text search
   query_embedding = embed(TextDoc(text='deodorant')).embedding
   matches = doc_index.find(query_embedding, search_field='embedding', limit=3)

   # Image search
   query_embedding = embed(ImageDoc(url='/path/to/query/image.jpg')).embedding
   matches = doc_index.find(query_embedding, search_field='embedding', limit=5)
   ```

## How It Works

1. **Data Loading**: Product data is loaded from a JSON file containing product names, prices, and image URLs.
2. **Image Downloading**: Product images are asynchronously downloaded and saved locally.
3. **Embedding Generation**: Each product image is embedded using the ImageBind model, which creates a unified representation for both images and text.
4. **Indexing**: The product embeddings are indexed using HNSW for efficient similarity search.
5. **Searching**: Users can search for products using either text descriptions or example images. The system finds the most similar products based on the embedded representations.

## Customization

- Adjust the `batch_size` variable to optimize memory usage and processing speed during indexing.
- Modify the `ProductDoc` class to include additional product attributes as needed.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## Acknowledgments

- [ImageBind](https://github.com/facebookresearch/ImageBind) by Facebook Research
- [DocArray](https://github.com/docarray/docarray) for efficient indexing and searching
- [pandas](https://pandas.pydata.org/) for data manipulation