---
title: デバイス プロパティの表示 (Windows Server 2003、Windows XP)
description: デバイスのプロパティの表現 (Windows Server 2003、Windows XP、および Windows 2000)
ms.assetid: 124172d7-52a4-423c-a1fd-eec554f328d6
keywords:
- デバイスのプロパティ表現 WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7099e50f751f2d618a829cf599d1fe2254cb3825
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387119"
---
# <a name="device-property-representations-windows-server-2003-windows-xp-and-windows-2000"></a>デバイスのプロパティの表現 (Windows Server 2003、Windows XP、および Windows 2000)


Windows Server 2003、Windows XP、および Windows 2000 をサポートしていない、[統一されたデバイス プロパティのモデル](unified-device-property-model--windows-vista-and-later-.md)その Windows Vista と Windows のサポートの以降のバージョン。 ただし、ほとんどの[デバイスのシステム定義のプロパティ](https://docs.microsoft.com/previous-versions/ff553413(v=vs.85))収録されているプロパティの統一されたデバイス モデルで Windows の以前のバージョンでサポートされている対応する表現があります。 Windows の以前のバージョン、方法は、デバイス プロパティが表され、プロパティにアクセスするためのメカニズムは、コンポーネントの種類とプロパティの型によって異なります。 これらの表現とメカニズム次に示します。

-   デバイス プロパティがへの入力パラメーターとして指定されているシステム定義の識別子によって表される、 [SetupAPI 関数](setupapi.md)デバイス プロパティにアクセスします。

-   デバイスのプロパティには、明示的な表現はありません。 ただし、デバイスのプロパティに関連付けられている情報を使用すると、SetupAPI 関数への呼び出しを取得できる、プラグ アンド プレイ (PnP) の構成マネージャーの機能。

-   デバイスのプロパティは、Windows レジストリの関数を使用してアクセスできるレジストリ エントリの値によって表されます。

-   INF ファイルのエントリの値は、デバイスのプロパティを変更します。

次のトピックでは、Windows Server 2003、Windows XP、および Windows 2000 でデバイスのプロパティにアクセスする方法についてを説明します。

[デバイスのプロパティを変更する INF ファイル エントリの値](inf-file-entry-values-that-modify-device-properties.md)

[SetupAPI とデバイス プロパティにアクセスする Configuration Manager を使用してください。](using-setupapi-and-configuration-manager-to-access-device-properties.md)

**注**   Windows の以前のバージョンとの互換性を維持するために Windows Vista およびそれ以降のバージョンもサポートしてこれらのメカニズムです。 ただし、Windows Vista およびそれ以降のバージョンでデバイスのプロパティにアクセスするのに、統一されたデバイス プロパティのモデルを使用する必要があります。

 

 

 





