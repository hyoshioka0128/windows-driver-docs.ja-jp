---
title: WMI のライブラリを使用してブロックを登録するには
description: WMI のライブラリを使用してブロックを登録するには
ms.assetid: 1f4b773d-ca24-47f5-87e8-84c98dad9267
keywords:
- WMI の WDK カーネルでは、WMI に登録します。
- WMI データ プロバイダーを登録します。
- WDK の WMI のデータ プロバイダー
- ドライバー WDK WMI の登録
- イベントは、WDK の WMI をブロックします。
- WDK の WMI をブロックします。
- IRP_MN_REGINFO
- IRP_MN_REGINFO_EX
- ブロックを登録します。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f343262d5e71fe5c3081920c66fbf21d209ca579
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556799"
---
# <a name="using-the-wmi-library-to-register-blocks"></a>WMI のライブラリを使用してブロックを登録するには





ドライバーは、WMI ライブラリを使用して処理するために[ **IRP\_MN\_REGINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff551731)と[ **IRP\_MN\_REGINFO\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff551734)要求のかどうか、動的なインスタンスの名前を使用しないまたは PDO またはドライバーの定義の基本名の文字列に基づいて静的インスタンス名を使用するブロックが登録されています。 この場合は、ドライバー。

1.  呼び出し[ **WmiSystemControl** ](https://msdn.microsoft.com/library/windows/hardware/ff565834)ドライバーのデバイス オブジェクトへのポインターにポインターを使用して、 [ **WMILIB\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff565813)構造、および IRP へのポインター

    **WMILIB\_コンテキスト**構造体を登録するブロックの数を示します (**GuidCount**) およびポイントの一覧に[ **WMIGUIDREGINFO**](https://msdn.microsoft.com/library/windows/hardware/ff565811)構造 (**GuidList**) インスタンス、および対応するブロックに関連する登録フラグの数、GUID を指定します。 ドライバーの必須のエントリ ポイントも定義と省略可能な*DpWmiXxx*コールバック ルーチン。

2.  WMI がドライバーを呼び出すときに[ *DpWmiQueryReginfo* ](https://msdn.microsoft.com/library/windows/hardware/ff544097) 、日常的なドライバーを指定します、ドライバーのレジストリ パス、その MOF リソース名、登録フラグに関連するすべてのブロック、および情報WMI では、ドライバーのデータ ブロックは、次のいずれかの名前のインスタンスに物理デバイス オブジェクトへのポインター、ドライバーに渡される[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)ルーチンまたは基になる文字列静的なインスタンス名です。

ドライバーのエントリ ポイントを初期化する必要があります、 *DpWmiXxx*コールバック ルーチン、 **WMILIB\_コンテキスト**呼び出す前に構造**WmiSystemControl**、初期化を延期することができますが、 **GuidCount**と**GuidList**で、 **WMILIB\_コンテキスト**WMI、ドライバーのを呼び出すまで構造体*DpWmiQueryReginfo*ルーチン。

 

 




