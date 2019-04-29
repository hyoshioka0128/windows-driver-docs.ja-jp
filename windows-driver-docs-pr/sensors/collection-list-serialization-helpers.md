---
title: コレクション リスト シリアル化ヘルパー
description: コレクションの一覧のシリアル化ヘルパー関数がセンサーでシリアル化に関連する操作を実行するため v2 センサー ドライバーによって使用される\_コレクション\_リストの構造体。
ms.assetid: 586FEDD7-6BA1-4E76-8E8D-E486F4711FAE
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: de8f12ff665197604096f632f043bacbc02e88f8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325316"
---
# <a name="collection-list-serialization-helpers"></a>コレクション リスト シリアル化ヘルパー


コレクション リストのシリアル化ヘルパー関数がでシリアル化関連の操作を実行するため、v2 センサー ドライバーで使用される[**センサー\_コレクション\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_collection_list)構造体。

ヘルパー関数は、センサー デバイス ドライバー ソフトウェア インターフェイス (DDSI) と共に使用されます。 これらのヘルパー関数は、アーキテクチャに依存しないためにを使用してデータ転送プロセスの境界を越えて安全です。 たとえば、DeviceIoControl の呼び出し中にこれらのヘルパー関数を使用しても安全です。

**SerializationBufferAllocate**

センサー DDSI による使用量

-   シリアル化のバッファーを割り当てるし、バッファーへのポインターを返します。

コメント

-   成功のバッファーの割り当ては、ステータスによって示されます\_[ok] の値。 それ以外の場合、適切な NTSTATUS エラー コードが返されます。

**SerializationBufferFree**

センサー DDSI による使用量

-   不要になったシリアル化するバッファーを解放します。

コメント

-   なし。

**CollectionsListGetSerializedSize**

センサー DDSI による使用量

-   シリアル化のバッファーのサイズを取得します。

コメント

-   バッファーのサイズは、ULONG 変数として返されます。

**CollectionsListSerializeToBuffer**

センサー DDSI による使用量

-   書き込み、 [**センサー\_コレクション\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_collection_list)情報をシリアル化のバッファー。

コメント

-   成功した書き込み操作はステータスによって示されます\_[ok] の値。 それ以外の場合、適切な NTSTATUS エラー コードが返されます。

**CollectionsListAllocateBufferAndSerialize**

センサー DDSI による使用量

-   シリアル化のバッファーを割り当ててし、書き込みます、 [**センサー\_コレクション\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_collection_list)バッファーへの情報。

コメント

-   バッファーの割り当てが成功した場合は、コレクションの一覧については、バッファーに書き込まれます。 それ以外の場合、書き込み操作は実行されませんし、適切な NTSTATUS エラー コードが返されます。

-   成功した書き込み操作はステータスによって示されます\_[ok] の値。 それ以外の場合、適切な NTSTATUS エラー コードが返されます。

**CollectionsListDeserializeFromBuffer**

センサー DDSI による使用量

-   読み取り[**センサー\_コレクション\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_collection_list)ソース バッファーからの情報。

コメント

-   読み取り操作が成功するとは、ステータスによって示されます\_[ok] の値。 それ以外の場合、適切な NTSTATUS エラー コードが返されます。

## <a name="requirements"></a>要件

|                          |                        |
|--------------------------|------------------------|
| サポートされている最小のクライアント | Windows 8.1            |
| サポートされている最小のサーバー | Windows Server 2012 R2 |
| Header                   | Sensorsutils.h         |

 

## <a name="related-topics"></a>関連トピック


[ヘルパー関数をマーシャ リング](marshalling-helper-functions.md)

 

 






