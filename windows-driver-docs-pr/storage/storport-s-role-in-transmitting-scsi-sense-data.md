---
title: SCSI センス データの送信に Storport のロール
description: SCSI センス データの送信に Storport のロール
ms.assetid: 18f2f4e0-f49b-4026-b18f-26b413f05970
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bcb042e3344cfeea2937fd2a8b707a29703d31e5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551962"
---
# <a name="storports-role-in-transmitting-scsi-sense-data"></a>SCSI センス データの送信に Storport のロール


Storport ドライバーは、scsi-3 要求センス データ用のデバイスが、クラス ドライバーなどの上位のコンポーネントが要求されるたびにクエリを実行する責任を負います。 センス データを要求する上位のコンポーネントがで指定された長さのバッファーを指定する必要があります、 **SenseInfoBufferLength**によって示される要求のセンス データを保持するために SRB のメンバー、 **SenseInfoBuffer** 、SRB のメンバー。 Storport は、これら 2 つのフィールドは、受信した各 SRB で定義されているかどうかを判断します。 Storport に定義されているターゲット コント ローラーでは、条件の確認を返します、SRB に応答するたびに scsi-3 要求センス データを提供します。

Storport が指すバッファーに格納する前に、適切な SRB 形式に要求のセンス データを変換することも、 **SenseInfoBuffer**します。

Storport IRP の完了時\_MJ\_、SRB に関連付けられている SCSI IRP、ことを返す要求の意味について論理 or 演算によって、SRB ことを示している必要があります\_状態\_AUTOSENSE\_有効フラグで、 **SrbStatus** SRB のメンバー。

 

 




