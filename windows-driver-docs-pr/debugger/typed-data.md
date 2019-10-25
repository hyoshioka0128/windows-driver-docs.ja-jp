---
title: 型指定されたデータ
description: 型指定されたデータ
ms.assetid: 44a84dfd-03f8-4d7b-8d71-e4b3ee23d105
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1b7d3c3bda27fe6c90774578c4d7f9d460bf50e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834262"
---
# <a name="typed-data"></a>型指定されたデータ


EngExtCpp extension framework には、ターゲットのメモリを操作するためのいくつかのクラスが用意されています。 [**ExtRemoteData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/engextcpp/nl-engextcpp-extremotedata)クラスは、ターゲットのメモリの小さな部分を表します。 このメモリの型がわかっている場合は、型指定された*データ*と呼ばれ、 [**extremotetyped**](https://docs.microsoft.com/windows-hardware/drivers/ddi/engextcpp/nl-engextcpp-extremotetyped)オブジェクトによって記述されます。

Windows リストは、 [**Extremotelist**](https://docs.microsoft.com/windows-hardware/drivers/ddi/engextcpp/nl-engextcpp-extremotelist)を使用して反復処理できます。リスト内のオブジェクトの型がわかっている場合は、 [**ExtRemoteTypedList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/engextcpp/nl-engextcpp-extremotetypedlist)です。

また、 [**Extextension**](https://msdn.microsoft.com/library/windows/hardware/ff543981)のクライアントオブジェクトと同様に、これらのクラスのインスタンスは、拡張ライブラリを使用して拡張コマンドを実行したり、出力用に構造体をフォーマットしたりする場合にのみ有効です **。  ** 特に、キャッシュしないでください。 クライアントオブジェクトが有効な場合の詳細については、「[クライアントオブジェクトとエンジン](client-objects-and-the-engine.md)」を参照してください。

 

### <a name="span-idremote_dataspanspan-idremote_dataspanremote-data"></a><span id="remote_data"></span><span id="REMOTE_DATA"></span>リモートデータ

リモートデータは、 [**ExtRemoteData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/engextcpp/nl-engextcpp-extremotedata)クラスを使用して処理する必要があります。 このクラスは、ターゲットのメモリの小さいセクションのラッパーです。 **ExtRemoteData**は、自動的にメモリを取得し、スローメソッドを使用して他の一般的な要求をラップします。

### <a name="span-idremote_typed_dataspanspan-idremote_typed_dataspanremote-typed-data"></a><span id="remote_typed_data"></span><span id="REMOTE_TYPED_DATA"></span>リモートで型指定されたデータ

リモートデータの型がわかっている場合は、 [**Extremotetyped**](https://docs.microsoft.com/windows-hardware/drivers/ddi/engextcpp/nl-engextcpp-extremotetyped)クラスを使用して処理する必要があります。 このクラスは、シンボルの型情報を使用して入力されたデータを認識する、拡張されたリモートデータオブジェクトです。 シンボルまたはキャストによって特定のオブジェクトに初期化されます。その後、指定された型のオブジェクトのように使用できます。

### <a name="span-idremote_listsspanspan-idremote_listsspanremote-lists"></a><span id="remote_lists"></span><span id="REMOTE_LISTS"></span>リモートリスト

リモートリストを処理するには、 [**Extremotelist**](https://docs.microsoft.com/windows-hardware/drivers/ddi/engextcpp/nl-engextcpp-extremotelist)クラスを使用します。 このクラスは、単一リンクリストまたはダブルリンクリストのいずれかに使用できます。 リストが二重にリンクされている場合は、前のポインターが次のポインターの直後にあると見なされます。 クラスには、リストを反復処理し、順方向および逆方向の両方のノードを取得できるメソッドが含まれています。 **Extremotelist**は、null で終わるリストまたは循環リストでも使用できます。

### <a name="span-idremote_typed_listsspanspan-idremote_typed_listsspanremote-typed-lists"></a><span id="remote_typed_lists"></span><span id="REMOTE_TYPED_LISTS"></span>リモート型のリスト

リスト内のノードの型がわかっている場合に、リモートリストを処理するには、 [**ExtRemoteTypedList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/engextcpp/nl-engextcpp-extremotetypedlist)クラスを使用します。 これは、 [**Extremotelist**](https://docs.microsoft.com/windows-hardware/drivers/ddi/engextcpp/nl-engextcpp-extremotelist)の拡張バージョンです。 **ExtRemoteTypedList**は、 **extremotelist**の基本的な機能に加えて、型情報からのリンクオフセットを自動的に決定します。

 

 





