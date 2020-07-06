---
title: コレクション リスト シリアル化ヘルパー
description: コレクションリストのシリアル化ヘルパー関数は、v2 センサードライバーによって使用され、センサーコレクションリスト構造に対するシリアル化関連の操作を実行し \_ \_ ます。
ms.assetid: 586FEDD7-6BA1-4E76-8E8D-E486F4711FAE
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: a5f249fd74d7082bde99c02b5c44d3957bd2cade
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85967895"
---
# <a name="collection-list-serialization-helpers"></a>コレクション リスト シリアル化ヘルパー


コレクションリストのシリアル化ヘルパー関数は、v2 センサードライバーによって使用され、[**センサー \_ コレクション \_ リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list)構造に対するシリアル化関連の操作を実行します。

ヘルパー関数は、センサーデバイスドライバーソフトウェアインターフェイス (DDSI) と共に使用されます。 また、これらのヘルパー関数はアーキテクチャに依存しないため、プロセスの境界を越えてデータを転送するために使用するのが安全です。 たとえば、DeviceIoControl を呼び出すと、これらのヘルパー関数を安全に使用できます。

**SerializationBufferAllocate**

センサー DDSI による使用量

-   シリアル化バッファーを割り当て、バッファーへのポインターを返します。

コメント

-   正常なバッファー割り当ては、ステータス OK 値によって示され \_ ます。 それ以外の場合は、適切な NTSTATUS エラーコードが返されます。

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

-   [**センサー \_ コレクション \_ リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list)情報をシリアル化バッファーに書き込みます。

コメント

-   正常な書き込み操作は、ステータス OK 値によって示され \_ ます。 それ以外の場合は、適切な NTSTATUS エラーコードが返されます。

**CollectionsListAllocateBufferAndSerialize**

センサー DDSI による使用量

-   シリアル化バッファーを割り当て、そのバッファーに[**センサー \_ コレクション \_ リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list)情報を書き込みます。

コメント

-   バッファー割り当てが成功した場合は、コレクションリストの情報がバッファーに書き込まれます。 それ以外の場合、書き込み操作は実行されず、適切な NTSTATUS エラーコードが返されます。

-   正常な書き込み操作は、ステータス OK 値によって示され \_ ます。 それ以外の場合は、適切な NTSTATUS エラーコードが返されます。

**CollectionsListDeserializeFromBuffer**

センサー DDSI による使用量

-   ソースバッファーから[**センサー \_ コレクション \_ リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list)情報を読み取ります。

コメント

-   正常な読み取り操作は、ステータス OK 値によって示され \_ ます。 それ以外の場合は、適切な NTSTATUS エラーコードが返されます。

## <a name="requirements"></a>要件

**サポートされている最低限のクライアント**: Windows 8.1

**サポートされている最小サーバー**: Windows Server 2012 R2

**ヘッダー**: Sensorsutils


 

## <a name="related-topics"></a>関連トピック


[マーシャリング ヘルパーの関数](marshalling-helper-functions.md)

 

 






