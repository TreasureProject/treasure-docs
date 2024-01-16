# Metadata Support

## Metadata Structure

**As you build and design your collections, please ensure that you abide by:**

* the [Non-Fungible Token (ERC-721)](https://eips.ethereum.org/EIPS/eip-721) and [Multi Token (ERC-1155)](https://eips.ethereum.org/EIPS/eip-1155) standards; and
* the [OpenSea Metadata Standards](https://docs.opensea.io/docs/metadata-standards) to design your metadata structure

Your collection's contract must return a valid URI for the `tokenURI()` (ERC721) or `uri()` (ERC1155) calls. Examples of valid token URIs include:

* A URL to an IPFS file (e.g., 'ipfs://Qm.......')
* A URL to an Arweave file (e.g., 'ar://....')
* An 'http://' or 'https://' URL.
* A base64 encoded JSON object (e.g., 'data:application/json;base64...')
* A UTF-8 encoded JSON object (e.g., 'data:application/json;utf8,....')

Example of JSON metadata AFTER its token URI is downloaded/decoded:

```jsx
{
  "description": "The Smol Brains are a dynamic PFP of a monkey whose head gets bigger the larger its IQ becomes.", 
  "external_url": "<https://smolverse.lol/smol-brains/3>", 
  "image": "ipfs://QmY71ban6QoWg9nbNwikk6wVWknj8NFBG8nMGHEuzwfAwf/3", 
  "name": "Smol Brains #3",
  "attributes": [ ... ], 
}
```

How each of these properties work:

<table data-header-hidden><thead><tr><th width="201">Property</th><th>Description</th></tr></thead><tbody><tr><td><strong>image</strong></td><td>This is the URL to the image of the item. Can be just about any type of image (including SVGs, which require explicit approval from the Trove team), and can be IPFS URLs or paths. Common image sizes are 350x350, 500x500 (please avoid images larger than 1500 pixels in any dimension).</td></tr><tr><td><strong>external_url</strong></td><td>This is the URL that will appear below the asset's image on Trove and will allow users to leave Trove and view the item on your site (if applicable).</td></tr><tr><td><strong>description</strong></td><td>A human readable description of the item. Markdown is supported.</td></tr><tr><td><strong>name</strong></td><td>Name of the item.</td></tr><tr><td><strong>attributes</strong></td><td>These are the attributes for the item, which will show up on the Trove page for the item. (see below)</td></tr><tr><td><strong>animation_url</strong></td><td><p>A URL to a multi-media attachment for the item.</p><ul><li>Supported animated images include GIF and WEBP.</li><li>Supported video formats include MP4.</li></ul></td></tr></tbody></table>

![](broken-reference)

### Supported Media Formats

* Static images (.png, .jpg, .gif, .svg, .webp)
* Animated images (.gif, .webp)
* Videos (.mp4)

### Attributes

For launch, Treasure will only support basic attributes displayed as a grid. Number ranges and more dynamic or visual representations of attributes will be implemented at a future date.

#### Attribute **Guidelines**

You should include string attributes as strings (with quotes), and numeric properties as either floats or integers so that Treasure can display them appropriately. String properties should be human-readable strings.

Attributes should take this form:

```jsx
{
  "attributes": [
    {
      "trait_type": "Background", 
      "value": "Mint"
    }, 
    {
      "trait_type": "Mushroom", 
      "value": "Blue"
    }, 
    {
      "trait_type": "Skin", 
      "value": "OG Green"
    }, 
    {
      "trait_type": "Clothes", 
      "value": "Hoodie - Grey"
    }, 
    {
      "trait_type": "Mouth", 
      "value": "Laugh - Teeth"
    },
    {
      "trait_type": "Level",
      "value": 3
    }
  ]
}
```

NOTE: any strings used in `trait_type` and `value` should exclude the characters `#`, `:`, and `,` (hash, colon, and comma). If they are present, they will be normalized to `_`.

### Image Versioning

At launch, Treasure will **NOT** support different image versions for NFTs.

### IPFS and Arweave URIs

Treasure will support the storage of NFT metadata in decentralized file networks.
