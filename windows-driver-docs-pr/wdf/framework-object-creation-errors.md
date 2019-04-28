---
title: フレームワーク オブジェクトの作成エラー
description: フレームワーク オブジェクトの作成エラー
ms.assetid: f5345c88-1c3a-4b32-9c93-c252713f7641
keywords:
- framework オブジェクト WDK KMDF、作成エラー
- WDK KMDF のエラー
- エラー WDK KMDF、framework のオブジェクトの作成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42e64de4ba719468dd713ad26e05e24866e7b100
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371024"
---
# <a name="framework-object-creation-errors"></a>フレームワーク オブジェクトの作成エラー


Framework のオブジェクトを作成するドライバーの試みが失敗した場合、オブジェクトの作成方法は、失敗の種類を示す NTSTATUS 値を返します。

ドライバーに無効な情報を指定する場合、 [ **WDF\_オブジェクト\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff552400)構造、フレームワークが返すことができます。

<a href="" id="status-wdf-object-attributes-invalid"></a>ステータス\_WDF\_オブジェクト\_属性\_が無効です  
ドライバーには、オブジェクト コンテキスト名が指定されたが、コンテキストのサイズは 0 です。

ドライバーは、コンテキスト サイズの上書き値を指定しは提供されませんでした、 [ **WDF\_オブジェクト\_コンテキスト\_型\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff552407)構造体。

指定されたドライバーを**ContextSizeOverride** WDF 値\_オブジェクト\_属性はより小さい**ContextSize** 、WDF のメンバー\_オブジェクト\_コンテキスト\_型\_情報構造体。

指定されたドライバー、 **ExecutionLevel** WDF 値\_オブジェクト\_が有効な値の範囲内にない属性です。

指定されたドライバー、 **SynchronizationScope** WDF 値\_オブジェクト\_が有効な値の範囲内にない属性です。

<a href="" id="status-wdf-parent-assignment-not-allowed"></a>ステータス\_WDF\_親\_割り当て\_いない\_許可  
ドライバーは、オブジェクトに親を割り当てようとしましたが、フレームワークには、ドライバー、オブジェクトの種類に親を割り当てるにはできません。

<a href="" id="status-wdf-parent-already-assigned"></a>ステータス\_WDF\_親\_ALREADY\_割り当て済み  
ドライバーは、オブジェクトに親を割り当てようとしましたが、親がオブジェクトに既に割り当てられています。

<a href="" id="status-wdf-parent-is-self"></a>ステータス\_WDF\_親\_IS\_セルフ  
ドライバーは、それ自身の親オブジェクトを作成しようとしました。

<a href="" id="status-wdf-synchronization-scope-invalid"></a>ステータス\_WDF\_同期\_スコープ\_が無効です  
指定されたドライバーを[ **WDF\_同期\_スコープ**](https://msdn.microsoft.com/library/windows/hardware/ff552518)-型指定された値は、オブジェクトの種類は無効です。

<a href="" id="status-wdf-execution-level-invalid"></a>ステータス\_WDF\_実行\_レベル\_が無効です  
指定されたドライバーを[ **WDF\_実行\_レベル**](https://msdn.microsoft.com/library/windows/hardware/ff551310)-型指定された値は、オブジェクトの種類は無効です。

場合、**サイズ**フレームワーク定義の構造体のメンバーが構造体の実際のサイズと一致しません、フレームワークは、状態を返すことができます\_情報\_長さ\_が一致しません。

状態を返せる場合は、フレームワークは、新しいオブジェクトのメモリを割り当てることができません、\_不十分\_リソース。

個々 のオブジェクトの作成方法が他に返す可能性がありますも[NTSTATUS 値](https://msdn.microsoft.com/library/windows/hardware/ff557697)します。 各作成メソッドの追加の戻り値の詳細については、メソッドのリファレンス ページを参照してください。

 

 





