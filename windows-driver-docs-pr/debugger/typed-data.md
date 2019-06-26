---
title: 型指定されたデータ
description: 型指定されたデータ
ms.assetid: 44a84dfd-03f8-4d7b-8d71-e4b3ee23d105
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c1c97f1ede75bc278c97f6dc28420bc97aa0107
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368637"
---
# <a name="typed-data"></a>型指定されたデータ


EngExtCpp の拡張機能フレームワークでは、ターゲットのメモリを操作するいくつかのクラスを提供します。 [ **ExtRemoteData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/engextcpp/nl-engextcpp-extremotedata)クラスがターゲットのメモリの一部について説明します。 このメモリの種類がわかっている場合、呼びます*型指定されたデータ*しで説明されているが[ **ExtRemoteTyped** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/engextcpp/nl-engextcpp-extremotetyped)オブジェクト。

キーを使用して場所を空ける Windows リストを反復処理できる[ **ExtRemoteList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/engextcpp/nl-engextcpp-extremotelist)と、リスト内のオブジェクトの種類がわかっている場合は[ **ExtRemoteTypedList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/engextcpp/nl-engextcpp-extremotetypedlist).

**注**  などのクライアント オブジェクトで[ **ExtExtension**](https://msdn.microsoft.com/library/windows/hardware/ff543981)、これらのクラスのインスタンスは、拡張ライブラリは、拡張機能のコマンドを実行するために使用中にのみ有効ですか形式の出力構造体。 具体的には、これらはキャッシュされません。 クライアント オブジェクトが有効な場合の詳細については、次を参照してください。[クライアント オブジェクトと、エンジン](client-objects-and-the-engine.md)、します。

 

### <a name="span-idremotedataspanspan-idremotedataspanremote-data"></a><span id="remote_data"></span><span id="REMOTE_DATA"></span>リモート データ

クラスを使用してリモート データを処理する必要があります[ **ExtRemoteData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/engextcpp/nl-engextcpp-extremotedata)します。 このクラスは、ターゲットのメモリの小さなセクションのラッパーです。 **ExtRemoteData**自動的にメモリを取得し、メソッドをスローすることで他の一般的な要求をラップします。

### <a name="span-idremotetypeddataspanspan-idremotetypeddataspanremote-typed-data"></a><span id="remote_typed_data"></span><span id="REMOTE_TYPED_DATA"></span>リモートの型指定されたデータ

リモート データの種類がわかっている場合、処理を使用して、 [ **ExtRemoteTyped** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/engextcpp/nl-engextcpp-extremotetyped)クラス。 このクラスは、シンボルから型情報の入力データで認識される強化されたリモート データ オブジェクトです。 シンボルまたはキャスト、その後、ように使用できる指定された型のオブジェクトで特定のオブジェクトに初期化されます。

### <a name="span-idremotelistsspanspan-idremotelistsspanremote-lists"></a><span id="remote_lists"></span><span id="REMOTE_LISTS"></span>リモートのリスト

リモートのリストを処理するために使用して、 [ **ExtRemoteList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/engextcpp/nl-engextcpp-extremotelist)クラス。 このクラスは、シングル リンクまたはダブルリンク リストで使用できます。 リストが二重にリンクされた場合、前のポインターは、次のポインターを直後と見なされます。 クラスには、リストを反復処理したり、前方と後方の両ノードを取得するメソッドが含まれています。 **ExtRemoteList**も null で終わるまたは循環リストで使用できます。

### <a name="span-idremotetypedlistsspanspan-idremotetypedlistsspanremote-typed-lists"></a><span id="remote_typed_lists"></span><span id="REMOTE_TYPED_LISTS"></span>リモートの型指定されたリスト

リスト内のノードの型がわかっている場合は、リモートのリストを処理するには、使用、 [ **ExtRemoteTypedList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/engextcpp/nl-engextcpp-extremotetypedlist)クラス。 これは、強化されたバージョンの[ **ExtRemoteList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/engextcpp/nl-engextcpp-extremotelist)します。 基本的な機能だけでなく**ExtRemoteList**、 **ExtRemoteTypedList**型情報からリンク オフセットが自動的に決定します。

 

 





