---
lab:
  title: Arbeiten mit Daten
ms.openlocfilehash: 6db1dd05ed150a1428ee355c932edc1082c1e3ba
ms.sourcegitcommit: 18f734eeb1031a9cb69c3b294632efd2e69324ac
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2021
ms.locfileid: "132832602"
---
# <a name="work-with-data"></a>Arbeiten mit Daten

Obwohl es recht üblich ist, mit Daten in ihrem lokalen Dateisystem zu arbeiten, kann es in einer Unternehmensumgebung effektiver sein, die Daten an einem zentralen Ort zu speichern, an dem mehrere Data Scientists und Machine Learning-Techniker darauf zugreifen können.

In dieser Übung befassen Sie sich mit *Datenspeichern* und *Datasets*. Hierbei handelt es sich um die primären Objekte, die zum Abstrahieren des Datenzugriffs in Azure Machine Learning verwendet werden.

## <a name="before-you-start"></a>Vorbereitung

Schließen Sie die Übung *[Erstellen eines Azure Machine Learning-Arbeitsbereichs](01-create-a-workspace.md)* ab, falls Sie das noch nicht getan haben, um einen Azure Machine Learning-Arbeitsbereich und eine Compute-Instanz zu erstellen und die für diese Übung benötigten Notebooks zu klonen.

## <a name="open-jupyter"></a>Öffnen von Jupyter

Sie können zwar die Seite **Notebooks** in Azure Machine Learning Studio zum Ausführen von Notebooks nutzen, doch erweist sich die Verwendung einer Notebookentwicklungsumgebung mit größerem Funktionsumfang wie *Jupyter* häufig als produktiver.

1. Zeigen Sie in [Azure Machine Learning Studio](https://ml.azure.com) die Seite **Compute** für Ihren Arbeitsbereich an, und starten Sie auf der Registerkarte **Compute-Instanzen** Ihre Compute-Instanz, falls diese noch nicht ausgeführt wird.
2. Wenn die Compute-Instanz ausgeführt wird, klicken Sie auf den Link **Jupyter**, um die Jupyter-Startseite auf einer neuen Browserregisterkarte zu öffnen.

## <a name="work-with-datastores-and-datasets"></a>Arbeiten mit Datenspeichern und Datasets

In dieser Übung wird der Code für das Arbeiten mit Daten in einem Notebook bereitgestellt.

1. Navigieren Sie auf der Jupyter-Startseite zum Ordner **/users/*Ihr-Benutzername*/mslearn-dp100**, in dem Sie das Notebook-Repository geklont haben, und öffnen Sie das Notebook **Work with Data** (Arbeiten mit Daten).
2. Lesen Sie dann die Hinweise im Notebook, und führen Sie die einzelnen Codezellen nacheinander aus.
3. Nachdem Sie den Code im Notebook ausgeführt haben, klicken Sie im Menü **Datei** auf **Schließen und anhalten**, um das Notebook zu schließen und den Python-Kernel herunterzufahren. Schließen Sie dann alle Jupyter-Browserregisterkarten.

## <a name="clean-up"></a>Bereinigung

Wenn Sie die Arbeit mit Azure Machine Learning vorerst beendet haben, wählen Sie in Azure Machine Learning Studio auf der Seite **Compute** auf der Registerkarte **Compute-Instanzen** Ihre Compute-Instanz aus, und klicken Sie auf **Beenden**, um sie herunterzufahren. Andernfalls führen Sie die Instanz für das nächste Lab weiter aus.

> **Hinweis**: Durch das Beenden Ihrer Compute-Instanz wird sichergestellt, dass Ihrem Abonnement keine Computeressourcen in Rechnung gestellt werden. Ihnen wird jedoch eine geringe Datenspeichermenge in Rechnung gestellt, solange der Azure Machine Learning-Arbeitsbereich in Ihrem Abonnement enthalten ist. Wenn Sie mit dem Erkunden von Azure Machine Learning fertig sind, können Sie Ihren Azure Machine Learning-Arbeitsbereich und die zugehörigen Ressourcen löschen. Wenn Sie jedoch weitere Labs in dieser Reihe durchführen möchten, müssen Sie die Übung *[Erstellen eines Azure Machine Learning-Arbeitsbereich](01-create-a-workspace.md)* wiederholen, um zunächst den Arbeitsbereich zu erstellen und die Umgebung vorzubereiten.