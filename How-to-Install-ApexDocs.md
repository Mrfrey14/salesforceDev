_**How to Run ApexDocs**_

1. Install Node JS: [Node JS Download](https://nodejs.org/en/#home-downloadhead)

2. Run the following command in Windows Powershell to install apexDocs: `npm install -g @cparra/apexdocs `

3. In your CLI (whether in your IDE or via Powershell) to run apexDocs on your apex classes (can be further customized, documentation on this command on the ApexDocs github page): apexdocs-generate -s [Path to directory of apex files you would like documentation generated for]  -c [path to the ApexDocsConfig.json file I provided for you]  -p public private

_**More information about ApexDocs is located within its git repository here: [ApexDocs](https://github.com/cesarParra/apexdocs)**_