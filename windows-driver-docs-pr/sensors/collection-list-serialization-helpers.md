---
title: コレクション リスト シリアル化ヘルパー
description: コレクションリストのシリアル化ヘルパー関数は、v2 センサードライバーによって使用され、センサー\_コレクション\_リスト構造体に対してシリアル化関連の操作を実行します。
ms.assetid: 586FEDD7-6BA1-4E76-8E8D-E486F4711FAE
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 222df31c118d39464502c139fd0e96d5e6d2f608
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842530"
---
# <a name="collection-list-serialization-helpers"></a>コレクション リスト シリアル化ヘルパー


コレクションリストのシリアル化ヘルパー関数は、v2 センサードライバーによって使用され、[**センサー\_コレクション\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list)構造体に対してシリアル化関連の操作を実行します。

ヘルパー関数は、センサーデバイスドライバーソフトウェアインターフェイス (DDSI) と共に使用されます。 また、これらのヘルパー関数はアーキテクチャに依存しないため、プロセスの境界を越えてデータを転送するために使用するのが安全です。 たとえば、DeviceIoControl を呼び出すと、これらのヘルパー関数を安全に使用できます。

**SerializationBufferAllocate**

センサー DDSI による使用量

-   シリアル化バッファーを割り当て、バッファーへのポインターを返します。

コメント

-   正常なバッファー割り当ては、ステータス\_OK 値によって示されます。 それ以外の場合は、適切な NTSTATUS エラーコードが返されます。

**SerializationBufferFree**

センサー DDSI による使用量

-   不要になったシリアル化バッファーを解放します。

コメント

-   なし。

**CollectionsListGetSerializedSize**

センサー DDSI による使用量

-   シリアル化バッファーのサイズを取得します。

コメント

-   バッファーサイズは ULONG 変数として返されます。

**CollectionsListSerializeToBuffer**

センサー DDSI による使用量

-   [**センサー\_コレクション\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list)情報をシリアル化バッファーに書き込みます。

コメント

-   書き込み操作が正常に行われた場合は、状態\_OK 値が示されます。 それ以外の場合は、適切な NTSTATUS エラーコードが返されます。

**CollectionsListAllocateBufferAndSerialize**

センサー DDSI による使用量

-   シリアル化バッファーを割り当て、[**センサー\_コレクション\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list)情報をバッファーに書き込みます。

コメント

-   バッファー割り当てが成功した場合は、コレクションリストの情報がバッファーに書き込まれます。 それ以外の場合、書き込み操作は実行されず、適切な NTSTATUS エラーコードが返されます。

-   書き込み操作が正常に行われた場合は、状態\_OK 値が示されます。 それ以外の場合は、適切な NTSTATUS エラーコードが返されます。

**CollectionsListDeserializeFromBuffer**

センサー DDSI による使用量

-   ソースバッファーから[**センサー\_コレクション\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list)情報を読み取ります。

コメント

-   正常な読み取り操作は、ステータス\_OK 値によって示されます。 それ以外の場合は、適切な NTSTATUS エラーコードが返されます。

## <a name="requirements"></a>要件

|                          |                        |
|--------------------------|------------------------|
| サポートされている最小のクライアント | Windows 8.1            |
| サポートされている最小のサーバー | Windows Server 2012 R2 |
| Header                   | Sensorsutils         |

 

## <a name="related-topics"></a>関連トピック


[マーシャリングヘルパー関数](marshalling-helper-functions.md)

 

 






