---
title: IRP_MJ_SHUTDOWN
description: IRP\_MJ\_シャット ダウン
ms.assetid: 4f7ba339-87f5-4011-8981-de6c31a9239a
keywords:
- IRP_MJ_SHUTDOWN インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- IRP_MJ_SHUTDOWN
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c85d543294cf537dd94aa186e6244d9a07c29634
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324455"
---
# <a name="irpmjshutdown"></a>IRP\_MJ\_シャット ダウン


## <a name="when-sent"></a>送信時


IRP\_MJ\_シャット ダウン要求は I/O マネージャーによって、またはファイル システム ドライバーによって、システムがシャット ダウンされるときに、送信されます。

## <a name="operation-file-system-drivers"></a>操作:ファイル システム ドライバー


ファイル システムが、必要なクリーンアップを実行する必要があり、ステータスの IRP の完了\_成功します。

## <a name="operation-file-system-filter-drivers"></a>操作:ファイル システム フィルター ドライバー


フィルター ドライバーは、スタックの次の下位ドライバーには、この IRP を渡す必要があります。

## <a name="parameters"></a>パラメーター


ファイル システムまたはフィルター ドライバーは呼び出し[ **IoGetCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549174)ポインターを取得する、独自の特定の IRP で[**場所スタック**](https://msdn.microsoft.com/library/windows/hardware/ff550659)、IRP として次の一覧に示すように*IrpSp*します。 (IRP が示した*Irp*)。ドライバーは IRP の IRP スタックの場所をシャット ダウン要求の処理では、次のメンバーで設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*デバイス オブジェクト*  
ターゲット デバイスのオブジェクトへのポインター。

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*  
ポインター、 [ **IO\_状態\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff550671)最終的な完了の状態と、要求された操作に関する情報を受け取る。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
IRP を指定します\_MJ\_設定\_シャット ダウンします。

## <a name="see-also"></a>関連項目


[**IO\_スタック\_場所**](https://msdn.microsoft.com/library/windows/hardware/ff550659)

[**IO\_状態\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff550671)

[**IoGetCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff549174)

[**IRP**](https://msdn.microsoft.com/library/windows/hardware/ff550694)

[**IRP\_MJ\_シャット ダウン (WDK カーネル リファレンス)**](https://msdn.microsoft.com/library/windows/hardware/ff550807)

 

 






