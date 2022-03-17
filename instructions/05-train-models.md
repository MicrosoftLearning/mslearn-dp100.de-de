---
lab:
  title: Trainieren von Modellen
ms.openlocfilehash: dffa9edda34c599dfbd372fe898ddcf955f6f200
ms.sourcegitcommit: 66d8872bc3d24c2121e225be132b56f4df7920ac
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2022
ms.locfileid: "138597261"
---
# <a name="train-models"></a>Trainieren von Modellen

Bei Machine Learning geht es in erster Linie um Trainingsmodelle, mit denen Sie Vorhersagedienste für Anwendungen bereitstellen können. In dieser Übung erfahren Sie, wie Sie Azure Machine Learning-Experimente zum Ausführen von Trainingsskripts verwenden und die resultierenden trainierten Modelle registrieren können.

## <a name="before-you-start"></a>Vorbereitung

Sofern nicht bereits geschehen, bearbeiten Sie die Übung *[Erstellen eines Azure Machine Learning-Arbeitsbereichs](01-create-a-workspace.md)* , um einen Azure Machine Learning-Arbeitsbereich und eine Compute-Instanz zu erstellen und die für diese Übung benötigten Notebooks zu klonen.

## <a name="open-jupyter"></a>Öffnen von Jupyter

Sie können zwar die Seite **Notebooks** in Azure Machine Learning Studio zum Ausführen von Notebooks nutzen, doch erweist sich die Verwendung einer Notebookentwicklungsumgebung mit größerem Funktionsumfang wie *Jupyter* häufig als produktiver.

1. Zeigen Sie in [Azure Machine Learning Studio](https://ml.azure.com) die Seite **Compute** für Ihren Arbeitsbereich an, und starten Sie auf der Registerkarte **Compute-Instanzen** Ihre Compute-Instanz, falls diese noch nicht ausgeführt wird.
2. Wenn die Compute-Instanz ausgeführt wird, klicken Sie auf den Link **Jupyter**, um die Jupyter-Startseite auf einer neuen Browserregisterkarte zu öffnen.

> **Tipp**: Haben Sie noch keine Erfahrung mit Python? Das [Cheat Sheet für Python](cheat-sheets/dp100-cheat-sheet-python.pdf) hilft Ihnen dabei, den Code zu verstehen. Haben Sie noch keine Erfahrung mit maschinellem Lernen? Unter [Übersicht über maschinelles Lernen](cheat-sheets/dp100-cheat-sheet-machine-learning.pdf) finden Sie eine vereinfachte Übersicht über den Machine-Learning-Prozess in Azure Machine Learning.

## <a name="train-models-using-the-azure-machine-learning-sdk"></a>Trainieren von Modellen mithilfe des Azure Machine Learning SDK

In dieser Übung wird der Code zum Trainieren von Modellen in einem Notebook bereitgestellt.

1. Navigieren Sie auf der Jupyter-Startseite zum Ordner **/users/*Ihr-Benutzername*/mslearn-dp100**, in dem Sie das Notebook-Repository geklont haben, und öffnen Sie das Notebook **Train Models** (Modelle trainieren).
2. Lesen Sie dann die Hinweise im Notebook, und führen Sie die einzelnen Codezellen nacheinander aus.
3. Nachdem Sie den Code im Notebook ausgeführt haben, klicken Sie im Menü **Datei** auf **Schließen und anhalten**, um das Notebook zu schließen und den Python-Kernel herunterzufahren. Schließen Sie dann alle Jupyter-Browserregisterkarten.

## <a name="clean-up"></a>Bereinigung

Wenn Sie die Arbeit mit Azure Machine Learning vorerst beendet haben, wählen Sie in Azure Machine Learning Studio auf der Seite **Compute** auf der Registerkarte **Compute-Instanzen** Ihre Compute-Instanz aus, und klicken Sie auf **Beenden**, um sie herunterzufahren. Andernfalls führen Sie die Instanz für das nächste Lab weiter aus.

> **Hinweis**: Durch das Beenden Ihrer Compute-Instanz wird sichergestellt, dass Ihrem Abonnement keine Computeressourcen in Rechnung gestellt werden. Ihnen wird jedoch eine geringe Datenspeichermenge in Rechnung gestellt, solange der Azure Machine Learning-Arbeitsbereich in Ihrem Abonnement enthalten ist. Wenn Sie mit dem Erkunden von Azure Machine Learning fertig sind, können Sie Ihren Azure Machine Learning-Arbeitsbereich und die zugehörigen Ressourcen löschen. Wenn Sie jedoch weitere Labs in dieser Reihe durchführen möchten, müssen Sie die Übung *[Erstellen eines Azure Machine Learning-Arbeitsbereichs](01-create-a-workspace.md)* wiederholen, um zunächst den Arbeitsbereich zu erstellen und die Umgebung vorzubereiten.