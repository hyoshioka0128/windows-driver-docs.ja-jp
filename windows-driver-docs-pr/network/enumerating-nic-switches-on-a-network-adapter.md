---
title: ネットワーク アダプターで NIC スイッチを列挙します。
description: ネットワーク アダプターで NIC スイッチを列挙します。
ms.assetid: 0799A879-2BC0-43C5-A6B6-6D46C74A26FB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5066ebde7ac30d395c459da0faa64e7993d01c2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531635"
---
# <a name="enumerating-nic-switches-on-a-network-adapter"></a>ネットワーク アダプターで NIC スイッチを列挙します。


上にあるドライバーやユーザー アプリケーションは、シングル ルート I/O 仮想化 (SR-IOV) をサポートするネットワーク アダプターで作成されたすべての NIC スイッチの一覧を取得できます。 ドライバーまたはアプリケーションのオブジェクト識別子 (OID) のクエリ要求を発行[OID\_NIC\_スイッチ\_ENUM\_スイッチ](https://msdn.microsoft.com/library/windows/hardware/hh451819)この一覧を取得します。

この OID 要求から正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造に含まれる、以下を含むバッファーへのポインター。

-   [ **NDIS\_NIC\_スイッチ\_情報\_配列**](https://msdn.microsoft.com/library/windows/hardware/hh451577)配列内の要素の数を定義する構造体。

-   配列の[ **NDIS\_NIC\_スイッチ\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451582)構造体。 各構造体には、ネットワーク アダプター上に作成する 1 つの NIC スイッチに関する情報が含まれています。

    **注**  NIC スイッチ、ネットワーク アダプターがない場合は、ドライバーの設定、 **NumElements**のメンバー、 [ **NDIS\_NIC\_スイッチ\_情報\_配列**](https://msdn.microsoft.com/library/windows/hardware/hh451577)構造体を 0、no [ **NDIS\_NIC\_スイッチ\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451582)構造体が返されます。

     

**注**  以降 Windows Server 2012 では、SR-IOV インターフェイスをサポートしています NIC スイッチが 1 つだけ、ネットワーク アダプター。 このスイッチと呼ばれる、 *NIC スイッチの既定*、NDIS によって参照されている\_既定\_スイッチ\_ID です。

 

NDIS ハンドル、 [OID\_NIC\_スイッチ\_ENUM\_スイッチ](https://msdn.microsoft.com/library/windows/hardware/hh451819)ミニポート ドライバーに要求します。 NDIS は、次のソースから保持されているデータの内部キャッシュから情報を返します。

-   レジストリの標準化された設定の SR-IOV キーワード。 これらのキーワードの詳細については、次を参照してください。 [SR-IOV の標準化された INF キーワード](standardized-inf-keywords-for-sr-iov.md)します。

-   OID 要求[OID\_NIC\_スイッチ\_作成\_スイッチ](https://msdn.microsoft.com/library/windows/hardware/hh451815)と[OID\_NIC\_スイッチ\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/hh451823).

**注**  NDIS は、スイッチの列挙型も用意されています、 **NicSwitchArray**内のメンバー、 [ **NDIS\_バインド\_パラメーター。**](https://msdn.microsoft.com/library/windows/hardware/ff564832)と[ **NDIS\_フィルター\_アタッチ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff565481)構造体。 上位のプロトコルとフィルター ドライバーがないため、問題を[OID\_NIC\_スイッチ\_ENUM\_スイッチ](https://msdn.microsoft.com/library/windows/hardware/hh451819)この情報を取得する要求。

 

 

 





