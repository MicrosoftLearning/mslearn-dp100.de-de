---
title: Online gehostete Anweisungen
permalink: index.html
layout: home
ms.openlocfilehash: a2eb157b1d188655f4cfbcc575befec4a2e9c623
ms.sourcegitcommit: 18f734eeb1031a9cb69c3b294632efd2e69324ac
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2021
ms.locfileid: "137894573"
---
# <a name="azure-machine-learning-exercises"></a>Azure Machine Learning: Übungen

Dieses Repository enthält die Labübungen für Microsoft-Kurs [Kurs DP-100T: *Entwerfen und Implementieren einer Data Science-Lösung in Azure*](https://docs.microsoft.com/learn/certifications/courses/dp-100t01) und die entsprechenden Selbststudiummodule zum [Erstellen und Betreiben von Machine Learning-Lösungen mit Azure Machine Learning](https://docs.microsoft.com/learn/paths/build-ai-solutions-with-azure-ml-service/). Diese Übungen begleiten die Lernmaterialen und erleichtern die praktische Anwendung der beschriebenen Technologien.

Sie benötigen ein Microsoft Azure-Abonnement für diese Übungen. Falls Sie kein Abonnement von Ihrem Kursleiter erhalten haben, können Sie sich unter [https://azure.microsoft.com](https://azure.microsoft.com) für eine kostenlose Testversion registrieren.

{% assign labs = site.pages | where_exp:"page", "page.url contains '/Instructions'" %}
| Übungen |
| ------- | 
{% for activity in labs  %}| [{{ activity.lab.title }}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}
