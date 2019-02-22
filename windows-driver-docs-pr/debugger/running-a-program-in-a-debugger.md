---
title: デバッガーでプログラムを実行します。
description: デバッガーでプログラムを実行します。
ms.assetid: e34b9560-33a2-47ed-83eb-84712b65a7f0
keywords:
- GFlags、デバッガーでプログラムを実行します。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59f2c31404bf960eaf6bf2110aa5bad874f33a00
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535765"
---
# <a name="running-a-program-in-a-debugger"></a>デバッガーでプログラムを実行します。


## <span id="ddk_running_a_program_in_a_debugger_dtools"></span><span id="DDK_RUNNING_A_PROGRAM_IN_A_DEBUGGER_DTOOLS"></span>


この機能は、常に、指定されたオプションのデバッガーで実行されるように、プログラムを構成します。 この設定は、レジストリに保存されます。 プログラムのすべての新しいインスタンスに影響し、変更するまで有効なままになります。

**デバッガーでプログラムを実行するには**

1.  をクリックして、**イメージ ファイル**タブ。

2.  **イメージ**ボックスで、実行可能ファイルまたはファイル名拡張子を含む DLL の名前を入力し、TAB キーを押します。

    上のチェック ボックスがアクティブになります、**イメージ ファイル**タブ。

3.  をクリックして、**デバッガー**チェック ボックスをオンにします。

    次のスクリーン ショットは、**デバッガー**チェック ボックスをオン、**イメージ ファイル**Windows Vista タブ。

    ![windows vista のイメージ ファイル タブで、デバッガー チェック ボックスのスクリーン ショット ](images/gflags-debugger.png)

4.  **デバッガー**ボックスに、パス (省略可能) を含む、デバッガーを実行するコマンドを入力し、デバッガーとパラメーターの名前。 たとえば、 **ntsd-d-g-g-x**または**c:\\デバッガー\\cdb.exe-g-g**します。

5.  **[適用]** をクリックします。

 

 





