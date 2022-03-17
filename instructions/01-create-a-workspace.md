---
lab:
  title: Erstellen eines Azure Machine Learning-Arbeitsbereichs
ms.openlocfilehash: 03b79f321ac3b5f7a5b9a03a3760db5649898eed
ms.sourcegitcommit: 66d8872bc3d24c2121e225be132b56f4df7920ac
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2022
ms.locfileid: "138597267"
---
# <a name="create-and-explore-an-azure-machine-learning-workspace"></a>Erstellen und Erkunden eines Azure Machine Learning-Arbeitsbereichs

In dieser Übung erstellen und untersuchen Sie einen Azure Machine Learning Arbeitsbereich.

## <a name="create-an-azure-machine-learning-workspace"></a>Erstellen eines Azure Machine Learning-Arbeitsbereichs

Wie der Name schon sagt, ist ein Arbeitsbereich ein zentraler Ort zum Verwalten aller Azure ML-Ressourcen, die Sie für die Arbeit an einem Machine Learning-Projekt benötigen.

1. Erstellen Sie im [Azure-Portal](https://portal.azure.com)eine neue **Machine Learning**-Ressource, und geben Sie dabei die folgenden Einstellungen an:

    - **Abonnement:** *Geben Sie Ihr Azure-Abonnement an.*
    - **Ressourcengruppe:** *Erstellen Sie eine Ressourcengruppe, oder wählen Sie eine vorhandene aus.*
    - **Arbeitsbereichsname**: *Geben Sie einen eindeutigen Namen für den Arbeitsbereich ein.*
    - **Region:** *Wählen Sie die nächstgelegene geografische Region aus.*
    - **Speicherkonto:** *Für Ihren Arbeitsbereich wird standardmäßig ein neues Speicherkonto erstellt.*
    - **Schlüsseltresor:** *Für Ihren Arbeitsbereich wird standardmäßig ein neuer Schlüsseltresor erstellt.*
    - **Application Insights:** *Für Ihren Arbeitsbereich wird standardmäßig eine neue Application Insights-Ressource erstellt.*
    - **Containerregistrierung:** Keine (*wird automatisch erstellt, wenn Sie das erste Mal ein Modell in einem Container bereitstellen*)

    > **Hinweis**: Beim Erstellen eines Azure Machine Learning-Arbeitsbereichs können Sie einige erweiterte Optionen verwenden, um den Zugriff über einen *privaten Endpunkt* einzuschränken und benutzerdefinierte Schlüssel für die Datenverschlüsselung anzugeben. Diese Optionen werden in dieser Übung nicht verwendet, aber Sie sollten wissen, dass es sie gibt.

2. Wenn der Arbeitsbereich und die zugehörigen Ressourcen erstellt wurden, zeigen Sie den Arbeitsbereich im Portal an.

## <a name="explore-azure-machine-learning-studio"></a>Erkunden von Azure Machine Learning Studio

Sie können einige Arbeitsbereichsressourcen im Azure-Portal verwalten. Für wissenschaftliche Fachkräfte für Daten enthält dieses Tool allerdings viele irrelevante Informationen und Links, die sich auf die Verwaltung allgemeiner Azure-Ressourcen beziehen. *Azure Machine Learning Studio* bietet ein dediziertes Webportal für die Arbeit mit Ihrem Arbeitsbereich.

1. Klicken Sie im Azure-Portal auf dem Blatt für Ihren Azure Machine Learning-Arbeitsbereich auf den Link zum Starten von Studio, oder öffnen Sie eine neue Browserregisterkarte mit [https://ml.azure.com](https://ml.azure.com). Wenn Sie dazu aufgefordert werden, melden Sie sich mit dem Microsoft-Konto an, das Sie in der vorherigen Aufgabe verwendet haben, und wählen Sie Ihr Azure-Abonnement und Ihren Arbeitsbereich aus.

    > **Tipp** Wenn Sie über mehrere Azure-Abonnements verfügen, müssen Sie das Azure-*Verzeichnis* auswählen, in dem das Abonnement definiert ist. Wählen Sie dann das Abonnement und schließlich den Arbeitsbereich aus.

2. Zeigen Sie die Azure Machine Learning Studio-Benutzeroberfläche für Ihren Arbeitsbereich an. Von hier aus können Sie alle Objekte in Ihrem Arbeitsbereich verwalten.
3. Klicken Sie in Azure Machine Learning Studio links oben auf das Symbol &#9776;, um die verschiedenen Seiten der Oberfläche anzuzeigen oder auszublenden. Sie können diese Seiten verwenden, um die Ressourcen in Ihrem Arbeitsbereich zu verwalten.

## <a name="create-a-compute-instance"></a>Erstellen einer Compute-Instanz

Einer der Vorteile von Azure Machine Learning ist die Möglichkeit zum Erstellen cloudbasierter Computeressourcen, auf denen Sie Experimente und Trainingsskripts im gewünschten Umfang ausführen können.

1. Zeigen Sie in Azure Machine Learning Studio die Seite **Compute** an. Hier verwalten Sie Computeressourcen für Ihre Data Science-Aktivitäten. Sie können vier Arten von Computeressourcen erstellen:
    - **Compute-Instanzen**: Entwicklungsarbeitsstationen, die wissenschaftliche Fachkräfte für Daten zum Arbeiten mit Daten und Modellen verwenden können
    - **Computecluster**: Skalierbare VM-Cluster für die bedarfsgesteuerte Verarbeitung von Experimentcode
    - **Rückschlusscluster**: Bereitstellungsziele für Vorhersagedienste, die Ihre trainierten Modelle verwenden
    - **Angefügte Computeressourcen**: Links zu anderen Azure-Computeressourcen, z. B. VMs oder Azure Databricks-Clustern

    Für diese Übung erstellen Sie eine Compute-Instanz, damit Sie Code in Ihrem Arbeitsbereich ausführen können.

2. Fügen Sie auf der Registerkarte **Compute-Instanzen** eine neue Compute-Instanz mit den folgenden Einstellungen hinzu. Sie verwenden diese als Arbeitsstation, um Code in Notebooks ausführen zu können.
    - **Computename:** *Geben Sie einen eindeutigen Namen ein.*
    - **Standort**: *Derselbe Standort wie Ihr Arbeitsbereich*
    - **VM-Typ**: CPU
    - **VM-Größe**: Standard_DS11_v2
    - **Insgesamt verfügbare Kontingente**: Zeigt die verfügbaren dedizierten Kerne an.
    - **Erweiterte Einstellungen anzeigen**: Beachten Sie die folgenden Einstellungen, aber wählen Sie sie nicht aus: 
        - **SSH-Zugriff aktivieren**: Nicht ausgewählt *(Sie können diese Option verwenden, um den Direktzugriff auf die VM über einen SSH-Client zu aktivieren.)*
        - **Virtuelles Netzwerk aktivieren**: Nicht ausgewählt *(Diese Option wird in der Regel in einer Unternehmensumgebung verwendet, um die Netzwerksicherheit zu verbessern.)*
        - **Einem anderen Benutzer zuweisen**: Nicht ausgewählt *(Anhand dieser Option können Sie eine Compute-Instanz einer wissenschaftlichen Fachkraft für Daten zuweisen.)* 3. Warten Sie, bis die Compute-Instanz gestartet wurde und den Status **Wird ausgeführt** aufweist.

> **Hinweis:** Compute-Instanzen und Computecluster basieren auf Standardimages virtueller Azure-Computer. Für diese Übung wird das Image *Standard_DS11_v2* empfohlen, um ein optimales Gleichgewicht zwischen Kosten und Leistung zu erzielen. Wenn Ihr Abonnement über ein Kontingent verfügt, das dieses Image nicht enthält, wählen Sie ein alternatives Image aus. Beachten Sie jedoch, dass ein größeres Image höhere Kosten verursachen kann und ein kleineres Image möglicherweise nicht ausreicht, um die Aufgaben auszuführen. Bitten Sie alternativ Ihren Azure-Administrator, Ihr Kontingent zu erhöhen.

## <a name="clone-and-run-a-notebook"></a>Klonen und Ausführen eines Notebooks

Viele Data Science- und Machine Learning-Experimente erfolgen durch die Ausführung von Code in *Notebooks*. Ihre Compute-Instanz umfasst vollständig ausgestattete Python-Notebookumgebungen (*Jupyter* und *JuypyterLab*), die Sie für umfangreiche Arbeiten verwenden können. Für die grundlegende Notebookbearbeitung können Sie die integrierte Seite **Notebooks** in Azure Machine Learning Studio nutzen.

1. Zeigen Sie in Azure Machine Learning Studio die Seite **Notebooks** an.
2. Wenn eine Meldung zur Beschreibung neuer Features angezeigt wird, schließen Sie sie.
3. Wählen Sie **Terminal** oder das Symbol **Terminal öffnen** aus, um ein Terminal zu öffnen, und stellen Sie sicher, dass **Compute** auf Ihre Compute-Instanz festgelegt ist und dass der aktuelle Pfad dem Ordner **/users/Ihr-Benutzername** entspricht.
4. Geben Sie den folgenden Befehl ein, um ein Git-Repository mit Notebooks, Daten und anderen Dateien in Ihrem Arbeitsbereich zu klonen:

    ```bash
    git clone https://github.com/MicrosoftLearning/mslearn-dp100 mslearn-dp100
    ```

4. Wenn der Befehl abgeschlossen ist, klicken Sie im Bereich **Meine Dateien** auf **&#8635;** , um die Ansicht zu aktualisieren und sicherzustellen, dass ein neuer Ordner **/users/*Ihr-Benutzername*/mslearn-dp100** erstellt wurde. Dieser Ordner enthält mehrere **IPYNB**-Notebookdateien.
5. Schließen Sie den Terminalbereich, um die Sitzung zu beenden.
6. Öffnen Sie im Ordner **/users/*Ihr-Benutzername*/mslearn-dp100** das Notebook **Get Started with Notebooks** (Erste Schritte mit Notebooks). Lesen Sie die Hinweise, und befolgen Sie die darin enthaltenen Anweisungen.

> **Tipp**: Wählen Sie zum Ausführen einer Codezelle die Zelle aus, die Sie ausführen möchten, und klicken Sie dann auf die Schaltfläche **&#9655;** , um die Ausführung zu starten. 

> **Haben Sie noch keine Erfahrung mit Python?** Das [Cheat Sheet für Python](cheat-sheets/dp100-cheat-sheet-python.pdf) hilft Ihnen dabei, den Code zu verstehen.

> **Haben Sie noch keine Erfahrung mit maschinellem Lernen?** Unter [Übersicht über maschinelles Lernen](cheat-sheets/dp100-cheat-sheet-machine-learning.pdf) finden Sie eine vereinfachte Übersicht über den Machine-Learning-Prozess in Azure Machine Learning.

## <a name="stop-your-compute-instance"></a>Beenden Ihrer Compute-Instanz

Wenn Sie Azure Machine Learning ausreichend erkundet haben, sollten Sie Ihre Compute-Instanz herunterfahren, um unnötige Gebühren in Ihrem Azure-Abonnement zu vermeiden.

1. Wählen Sie in Azure Machine Learning Studio auf der Seite **Compute** Ihre Compute-Instanz aus.
2. Klicken Sie auf **Beenden**, um Ihre Compute-Instanz zu beenden. Nach dem Herunterfahren ändert sich der Status in **Beendet**.

> **Hinweis**: Durch das Beenden Ihrer Computeressourcen wird sichergestellt, dass Ihrem Abonnement keine Computeressourcen in Rechnung gestellt werden. Ihnen wird jedoch eine geringe Datenspeichermenge in Rechnung gestellt, solange der Azure Machine Learning-Arbeitsbereich in Ihrem Abonnement enthalten ist. Wenn Sie mit dem Erkunden von Azure Machine Learning fertig sind, können Sie Ihren Azure Machine Learning-Arbeitsbereich und die zugehörigen Ressourcen löschen. Wenn Sie jedoch weitere Labs in dieser Reihe abschließen möchten, müssen Sie dieses Lab wiederholen, um zuerst den Arbeitsbereich zu erstellen und die Umgebung vorzubereiten.
