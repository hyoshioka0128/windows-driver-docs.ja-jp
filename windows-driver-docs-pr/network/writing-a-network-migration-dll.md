---
title: ネットワーク移行 DLL の作成
description: ネットワーク移行 DLL の作成
ms.assetid: a6a9e57a-cc39-4cdf-a374-4791ddd4a5da
keywords:
- DLL の WDK のネットワーク移行
- コンポーネントのアップグレード WDK のネットワーク、ネットワークの移行 DLL
- WDK のネットワーク コンポーネントをアップグレードするには、ネットワークの移行 DLL
- DLL の WDK ネットワークの移行
- ネットワーク移行 DLL の作成
- WDK の Dll のネットワーク移行
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6dab9f0c118ba47e843fbb3f03deac5abe543f1c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531843"
---
# <a name="writing-a-network-migration-dll"></a>ネットワーク移行 DLL の作成





**注**  Microsoft Windows XP では、ベンダーから提供されたネットワークのアップグレードはサポートされていない (SP1 以降)、Microsoft Windows Server 2003、および以降のオペレーティング システム。

 

ネットワーク移行 DLL は、Microsoft Windows NT 3.51 または Windows 2000 またはそれ以降の Windows NT 4.0 から 1 つまたは複数のネットワーク コンポーネントのパラメーターの値を移行します。

ネットワーク移行 DLL が必要です。

-   **アップグレード前のオペレーティング システム (Windows NT 3.51 または Windows 4.0) の下で読み込み**

    DLL は、Windows 2000 に固有またはそれ以降、関数を呼び出すことはできませんまたは Windows 2000 に固有またはそれ以降の機能を使用します。 Postupgrade (フル インストール モード) フェーズでは、DLL を実行する場合は、Windows 2000 と以降のオペレーティング システムに読み込む必要がありますも。

-   **エクスポート、** [ **PreUpgradeInitialize**](https://msdn.microsoft.com/library/windows/hardware/ff562439)**と**[**DoPreUpgradeProcessing** ](https://msdn.microsoft.com/library/windows/hardware/ff545634)**関数**

    DLL を GUI モードのフェーズで実行している場合はエクスポートする必要があります、 [ **PostUpgradeInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff562410)と[**発生**](https://msdn.microsoft.com/library/windows/hardware/ff545629)関数としてまぁ。

-   **Winnt32 フェーズ中に元に戻せない変更を加えない**

    DLL には、ファイルを削除またはユーザーのネットワーク コンポーネントやオペレーティング システムのアップグレードをキャンセルすることができますので、このフェーズ中にレジストリ キーを変更するなど、元に戻せない変更しないようにする必要があります。 ただし、NetSetup への呼び出しで指定された一時作業ディレクトリ内のファイルを変更できます、DLL **PreUpgradeInitialize**します。

 

 





