---
title: オーディオ ドライバー オブジェクトの作成
description: オーディオ ドライバー オブジェクトの作成
ms.assetid: c5d1b1b6-fc47-4227-bcca-1119488dce3b
keywords:
- オーディオ ドライバー オブジェクト WDK
- COM オブジェクトの作成の WDK オーディオ
- オブジェクトの WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f086bce6c2bdc411a8d968bb819892f45fcb0c34
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333963"
---
# <a name="creating-audio-driver-objects"></a>オーディオ ドライバー オブジェクトの作成


## <span id="creating_audio_driver_objects"></span><span id="CREATING_AUDIO_DRIVER_OBJECTS"></span>


などの関数を使用して、ユーザー モードで COM オブジェクトが作成されます**CoCreateInstance** (Microsoft Windows SDK のドキュメントで説明)、クライアントは、オブジェクトに必要なメモリの割り当て方法を認識します。 カーネル モードで、場所のメモリの割り当て傾向にあります厳重に管理する、オブジェクトの作成のさまざまなメソッドが必要です。

定義されているオーディオ ドライバー モデルは、COM インターフェイスの概念を使用して、 **IUnknown**インターフェイス。 ただし、オーディオ ドライバーは、レジストリにアクセスするか、インプロセス サーバーなどのメカニズムを使用するには必要ではありません。 ミニポート ドライバーは、集計をサポートする必要はありません。

慣例により、常にオブジェクトの特定のクラスを作成するための関数は、同じフォームを受け取ります。

```cpp
NTSTATUS CreateMyObject(
   OUT PUNKNOWN  *Unknown,
   IN REFGUID ClassId,
   IN PUNKNOWN OuterUnknown OPTIONAL,
   IN POOL_TYPE PoolType
 );
```

### <a name="span-idparametersspanspan-idparametersspanparameters"></a><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター

<span id="Unknown"></span><span id="unknown"></span><span id="UNKNOWN"></span>*不明*  
ポインターへのポインター、 **IUnknown**インターフェイス。 関数を使用して新しく作成されたオブジェクトへの参照を出力する*不明な*します。

<span id="ClassId"></span><span id="classid"></span><span id="CLASSID"></span>*ClassId*  
クラスが参照渡しの GUID を指定します。 このパラメーターは、関数は、複数のクラスのオブジェクトを作成する場合にのみ使用されます。 設定されている場合は、 **NULL**します。

<span id="OuterUnknown"></span><span id="outerunknown"></span><span id="OUTERUNKNOWN"></span>*OuterUnknown*  
指定します、 **IUnknown**新しいオブジェクトを集約するためのインターフェイス。 このパラメーターに設定できます**NULL**を集計が必要ないことを示します。

<span id="PoolType"></span><span id="pooltype"></span><span id="POOLTYPE"></span>*PoolType*  
元のオブジェクトが割り当てられるメモリ プールの種類を指定します (を参照してください[**プール\_型**](https://msdn.microsoft.com/library/windows/hardware/ff559707))。

最初の 3 つのパラメーターは、COM のパラメーターと同じ**CoCreateInstance**関数。 この種類の作成機能の例は、次を参照してください。、 **CreateMiniportMidiFM** Fmsynth サンプル オーディオ ドライバー Microsoft Windows Driver Kit (WDK) での関数。

別の規則は、新規を提供する*Xxx*クラスの関数。 このような関数のインスタンスを作成する簡単な方法を提供する (作成し、初期化) 次の例に示すように、オブジェクト。

```cpp
NTSTATUS NewMyObject(
 OUT PMYINTERFACE  *InterfacePointer,
 IN PUNKNOWN  OuterUnknown OPTIONAL,
 IN POOL_TYPE  PoolType,
  // ...more parameters
 );
```

NewMyObject 関数は、作成しオブジェクトを初期化しにインターフェイス ポインターを渡します。 新規のプロトタイプは、初期化パラメーターは、クラスに固有であるため*Xxx*関数。 新しい*Xxx*関数オブジェクトのコンス トラクターに簡単にアクセスを提供します。

新規の例については*Xxx*関数のこの種類は、次を参照してください。 [ **PcNewDmaChannel**](https://msdn.microsoft.com/library/windows/hardware/ff537712)します。

 

 




