# terraform graph

**The terraform graph command give you a graph how your infrastructure resources are connected, helping you see how everything fits together.**

## How to use

- `terraform graph | dot -Tpdf > graph.pdf` run this command in the directory where your terraform files are located.
- This command will create a pdf file of your infrastructure and describe your infrastructure in a one image.