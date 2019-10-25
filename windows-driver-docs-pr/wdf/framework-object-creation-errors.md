---
title: フレームワーク オブジェクトの作成エラー
description: フレームワーク オブジェクトの作成エラー
ms.assetid: f5345c88-1c3a-4b32-9c93-c252713f7641
keywords:
- フレームワークオブジェクト WDK KMDF、作成エラー
- WDK KMDF エラー
- エラー WDK KMDF、フレームワークオブジェクトの作成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e652cf8a8e26819952056657c13e69f9db214bba
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843121"
---
# <a name="framework-object-creation-errors"></a>フレームワーク オブジェクトの作成エラー


ドライバーのフレームワークオブジェクト作成の試行が失敗した場合、オブジェクトの作成メソッドは、エラーの種類を示す NTSTATUS 値を返します。

ドライバーで[**WDF\_オブジェクト\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)構造に無効な情報が指定されている場合、フレームワークは次を返すことができます。

<a href="" id="status-wdf-object-attributes-invalid"></a>ステータス\_WDF\_オブジェクト\_属性\_無効  
ドライバーでオブジェクトコンテキスト名が指定されましたが、コンテキストサイズが0です。

ドライバーでコンテキストサイズのオーバーライド値が指定されましたが、[**コンテキスト\_型\_INFO 構造体\_WDF\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_context_type_info)が提供されませんでした。

ドライバーは、WDF\_オブジェクトの**contextsize**メンバーよりも小さい属性\_WDF\_オブジェクトの**contextsizeoverride**値を指定しました。\_コンテキスト\_型\_INFO 構造体です。

ドライバーは、有効な値の範囲内にない属性\_、WDF\_オブジェクトの**Executionlevel**値を指定しました。

ドライバーは、有効な値の範囲内にない属性\_、WDF\_オブジェクトの**同期スコープ**値を指定しました。

<a href="" id="status-wdf-parent-assignment-not-allowed"></a>状態\_WDF\_親\_割り当て\_許可さ\_れていません  
ドライバーがオブジェクトに親を割り当てようとしましたが、フレームワークでは、ドライバーが親をオブジェクトの種類に割り当てることを許可していません。

<a href="" id="status-wdf-parent-already-assigned"></a>状態\_WDF\_親\_既に割り当てられて\_います  
ドライバーがオブジェクトに親を割り当てようとしましたが、親が既にオブジェクトに割り当てられています。

<a href="" id="status-wdf-parent-is-self"></a>状態\_WDF\_親\_は自己\_  
ドライバーは、オブジェクトをその親に設定しようとしました。

<a href="" id="status-wdf-synchronization-scope-invalid"></a>状態\_WDF\_同期\_スコープ\_無効  
ドライバーによって、オブジェクトの種類に対して無効なスコープ型の値[ **\_WDF\_同期**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ne-wdfobject-_wdf_synchronization_scope)が指定されました。

<a href="" id="status-wdf-execution-level-invalid"></a>ステータス\_WDF\_実行\_レベル\_無効  
ドライバーは、オブジェクトの種類に対して無効なレベル型の値[ **\_WDF\_実行**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ne-wdfobject-_wdf_execution_level)を指定しました。

フレームワーク定義の構造体の**サイズ**メンバーが構造体の実際のサイズと一致しない場合、フレームワークはステータス\_情報\_長さ\_不一致を返すことができます。

フレームワークが新しいオブジェクトにメモリを割り当てられない場合は、状態\_リソース\_不足している可能性があります。

個々のオブジェクトの作成方法では、追加の[NTSTATUS 値](https://docs.microsoft.com/windows-hardware/drivers/kernel/ntstatus-values)も返される場合があります。 各作成メソッドの追加の戻り値の詳細については、メソッドのリファレンスページを参照してください。

 

 





