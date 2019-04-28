---
title: ドライバー パッケージの更新バージョンのインストール
description: ドライバー パッケージの更新バージョンのインストール
ms.assetid: c2138956-a036-410d-b34e-b7b6efbcbace
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b88fdee7713ffa0602708b0215462654cc98b852
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366538"
---
# <a name="installing-the-updated-version-of-the-driver-package"></a>ドライバー パッケージの更新バージョンのインストール


したら[ランクのドライバーの署名に Windows を同じように構成](configuring-windows-to-rank-driver-signatures-equally.md)、受信トレイのドライバーのプライベート ビルドをインストールするには、ターゲット システムにします。 プライベート ビルドをインストールするには、次の手順を完了します。

1.  追加、[ドライバー パッケージ](driver-packages.md)ドライバーを使用して、格納、 [PnPUtil](https://msdn.microsoft.com/library/windows/hardware/ff550419) Windows Vista 以降のバージョンの Windows で提供されるユーティリティです。 次に、例を示します。

    ```cpp
    pnputil.exe -a  sample.inf
    ```

2.  デバイスまたは更新されたドライバー パッケージによってインストールされているデバイスのクラスを削除するのにには、DevCon 削除コマンドを使用します。 すべてまたは一部を使用して、デバイスまたはデバイス クラスを指定する[ハードウェア ID](hardware-ids.md)、[互換性 ID](compatible-ids.md)、またはデバイスのデバイス インスタンス ID。 次に、例を示します。

    ```cpp
    devcon remove "PCI\VEN_8086&DEV_7110"
    ```

    システムの再起動後にデバイスを再インストール時に、新しいドライバーが自動的に読み込まれます。 DevCon システムを自動的に再起動するのには、再起動の条件付きパラメーターを追加します (**/r**) を削除 コマンド。

    **注**  、 [DevCon](https://msdn.microsoft.com/library/windows/hardware/ff544707) WDK でツールが用意されています。 そのコマンドの詳細については、次を参照してください。 [DevCon コマンド](https://msdn.microsoft.com/library/windows/hardware/ff544766)します。

     

DevCon 削除コマンドの代替では、更新、[ドライバー パッケージ](driver-packages.md)次のいずれかを使用しています。

-   デバイス上の「ドライバーの更新」操作を実行するデバイス マネージャーです。

    デバイス マネージャーのウィンドウ内で、デバイスの名前またはアイコンを右クリックし、**プロパティ**します。 **プロパティ**ウィンドウがドライバー タブをクリックし、クリックして、**ドライバーの更新**ボタンをクリックします。

-   更新プログラムの DevCon コマンド。 このコマンドの詳細については、次を参照してください。 [ **DevCon コマンド**](https://msdn.microsoft.com/library/windows/hardware/ff544766)します。

 

 





