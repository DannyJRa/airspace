---
title: DSVM Part1
author: DannyJRa
date: '2020-03-01'
categories:
  - Cloud
tags:
  - Azure
hidden: false
image: images/blog/blog-post-1.jpg
share: false
output:
  html_document:
    keep_md: yes
    theme: cerulean
    highlight: tango
    code_folding: show
    toc: yes
    toc_float: yes
  pdf_document:
    number_sections: yes
geometry: margin = 1.2in
fontsize: 10pt
always_allow_html: yes
type: post
---




DSVM Part 1 thftz tz fz  



<a href="https://themes.gohugo.io//theme/airspace-hugo/blog/blog-post-1/" class="post-social-share">Continue Reading</a>



>The Windows Data Science Virtual Machine (DSVM) is a powerful data science development environment that enables you to perform various data exploration and modeling tasks. The environment comes already built and bundled with several popular data analytics tools that make it easy to get started quickly with your analysis for On-premises, Cloud or hybrid deployments. The DSVM works closely with many Azure services and is able to read and process data that is already stored on Azure, in Azure SQL Data Warehouse, Azure Data Lake, Azure Storage, or in Azure Cosmos DB. It can also leverage other analytics tools such as Azure Machine Learning and Azure Data Factory.[^1]

In this article, I will adopt the tutorial to needs and learn how to use Azure (Linux) DSVM to perform various data science tasks and interact with other Azure services. Here are some of the things you can do on the DSVM:

1. Explore data and develop models locally on the DSVM using RStudio
2.  Use a Jupyter notebook to experiment with your data on a browser using Python 2, Python 3, Microsoft R an enterprise ready version of R designed for performance
3. Deploy models built using R and Python on Azure Machine Learning so client applications can access your models using a simple web service interface
4. Administer your Azure resources using Azure portal or Powershell
5. Extend your storage space and share large-scale datasets / code across your whole team by creating an Azure File storage as a mountable drive on your DSVM
6. Share code with your team using GitHub and access your repository using the pre-installed Git clients - Git Bash, Git GUI.
7. Access various Azure data and analytics services like Azure blob storage, Azure Data Lake, Azure HDInsight (Hadoop), Azure Cosmos DB, Azure SQL Data Warehouse & databases
8. Build reports and dashboard using the Power BI Desktop pre-installed on the DSVM and deploy them on the cloud
9. Dynamically scale your DSVM to meet your project needs
10. Install additional tools on your virtual machine



Lorem ipsum dolor sit amet, consectetur adipisicing elit. Velit vitae placeat ad architecto nostrum asperiores
vel aperiam, veniam eum nulla. Maxime cum magnam, adipisci architecto quibusdam cumque veniam fugiat quae. Lorem
ipsum dolor sit amet, consectetur adipisicing elit. Odio vitae ab doloremque accusamus sit, eos dolorum officiis
a perspiciatis aliquid. Lorem ipsum dolor sit amet, consectetur adipisicing elit. Quod, facere. 

> Lid est laborum dolo rumes fugats untras. Etharums ser quidem rerum facilis dolores nemis omnis fugats vitaes
nemo minima rerums unsers sadips amets.. Sed ut perspiciatis unde omnis iste natus error

Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laborum illo deserunt necessitatibus quibusdam sint,
eos explicabo tenetur molestiae vero facere, aspernatur sit mollitia perferendis reiciendis. Deleniti magni
explicabo sed alias fugit amet animi molestias ipsum maiores. Praesentium sint, id laborum quos. Tempora
inventore est, dolor corporis quis doloremque nostrum, eos velit culpa quasi labore. Provident laborum porro
nihil iste, magnam officia nemo praesentium autem, libero vel officiis. Omnis pariatur nam voluptatem voluptate
at officia repellat ea beatae eligendi? Mollitia error saepe, aperiam facere. Optio maiores deleniti veritatis
eaque commodi atque aperiam, debitis iste alias eligendi ut facilis earum! Impedit, tempore.

```
  .blog-classic {
  margin-bottom: 70px;
  padding-bottom: 70px;
  border-bottom: 1px solid #efefef;
  }
```

Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ex error esse a dolore, architecto sapiente, aliquid
commodi, laudantium eius nemo enim. Enim, fugit voluptatem rem molestiae. Sed totam quis accusantium iste
nesciunt id exercitationem cumque repudiandae voluptas perspiciatis, consequatur quasi, molestias, culpa odio
adipisci. Nesciunt optio fugiat iste quam modi, ex vitae odio pariatur! Corrupti explicabo at harum qui
doloribus, sit dicta nemo, dolor, enim eum molestias fugiat obcaecati autem eligendi? Nisi delectus eaque
architecto voluptatibus, unde sit minus quae quod eligendi soluta recusandae doloribus, officia, veritatis
voluptatum eius aliquam quos. Consectetur, nisi? Veritatis totam, unde nostrum exercitationem tempora suscipit,
molestias, deserunt ipsum laborum aut iste eaque? Vitae delectus dicta maxime non mollitia? Sapiente eos a quia
eligendi deserunt repudiandae modi molestias tenetur autem pariatur ullam itaque, quas eveniet, illo quam rerum
ex obcaecati voluptatum nesciunt incidunt culpa provident illum soluta. Voluptas possimus nesciunt inventore
perspiciatis neque fugiat, magnam natus repellendus praesentium eum voluptatum, alias incidunt, tempora
reprehenderit recusandae et numquam itaque ratione dolor voluptatibus in commodi ut! Neque deserunt nostrum
commodi dolor natus quo, non vitae deleniti, vero voluptatem error aspernatur veniam expedita numquam amet quia
in dolores velit esse molestiae! Iusto architecto accusantium quisquam recusandae quod vero quia.