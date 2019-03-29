---
title: WDM ドライバーについての WMI の要件
description: WDM ドライバーについての WMI の要件
ms.assetid: 8290e570-acd9-4047-bd0b-c1c74847f243
keywords:
- WMI の WDK カーネル、WDM ドライバー
- WDM ドライバー WDK WMI
- Irp WDK WMI
- WDK の WMI の要求
- WMI の WDK カーネルでは、要求
- WDK の WMI のデータ プロバイダー
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4e9121c10cd0dd8dcf45da939bc079140575982
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578437"
---
# <a name="wmi-requirements-for-wdm-drivers"></a>WDM ドライバーについての WMI の要件





Irp を処理するドライバーは WMI で登録を*データ プロバイダー*します。 システムが指定したストレージ ポート ドライバー、クラスのドライバーおよび NDIS プロトコル ドライバーは、このカテゴリに分類されます。 WMI データ プロバイダーとして登録する方法の詳細については、次を参照してください。 [WMI データ プロバイダーとして登録する](registering-as-a-wmi-data-provider.md)します。

Irp を処理しないドライバーをドライバー スタックで、次の下位ドライバーへの WMI 要求を転送だけです。 次の下位ドライバーでは、WMI で登録し、最初のドライバーの代わりに WMI 要求を処理します。 たとえば、SCSI ミニポート ドライバーおよび NDIS ミニポート ドライバー WMI プロバイダーとして登録でき、対応するクラス ドライバーに WMI データを提供できます。

WMI データ クラスまたはポートのドライバーを提供するドライバーには、クラスまたはポートのドライバーで定義されているドライバー固有の種類の WMI インターフェイスをサポートする必要があります。 たとえば、SCSI ミニポート ドライバーを設定する必要があります**WmiDataProvider**に**TRUE**で、 [**ポート\_構成\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff563900)構造体し、処理 SRB\_関数\_SCSI ポート ドライバーからの WMI 要求。

同様に、カスタム データ ブロックを定義する接続指向の NDIS ミニポート ドライバーがサポートする必要があります[OID\_GEN\_CO\_サポートされている\_GUID](https://msdn.microsoft.com/library/windows/hardware/ff569566)、それ以外の NDIS これらの Oid をマップします。OID から返される状態インジケーターと\_GEN\_サポートされている\_NDIS によって定義されているは一般的なと既知の Guid に NDIS をリストします。

次のセクションでは、ドライバーでは Irp を処理する WMI をサポートする方法について説明します。

 

 




