---
title: オーディオ ドライバー オブジェクトの作成
description: オーディオ ドライバー オブジェクトの作成
ms.assetid: c5d1b1b6-fc47-4227-bcca-1119488dce3b
keywords:
- オーディオドライバーオブジェクト WDK
- COM オブジェクト作成 WDK オーディオ
- オブジェクト WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c95e9e75b0c49d6c3d1d4d42636e94e7f2b3c0d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833586"
---
# <a name="creating-audio-driver-objects"></a>オーディオ ドライバー オブジェクトの作成


## <span id="creating_audio_driver_objects"></span><span id="CREATING_AUDIO_DRIVER_OBJECTS"></span>


ユーザーモードでは、COM オブジェクトは**CoCreateInstance** (Microsoft Windows SDK ドキュメントで説明されています) などの関数を使用して作成されます。この場合、クライアントはオブジェクトに必要なメモリがどのように割り当てられているかを認識しません。 ただし、カーネルモードでは、メモリの割り当てが厳密に制御される傾向があるため、別のオブジェクト作成方法が必要になります。

オーディオドライバーモデルは、 **IUnknown**インターフェイスの定義に従って、COM インターフェイスの概念を使用します。 ただし、レジストリにアクセスしたり、インプロセスサーバーなどのメカニズムを使用したりするために、オーディオドライバーは必要ありません。 ミニポートドライバーは、集計をサポートするためには必要ありません。

慣例により、オブジェクトの特定のクラスを作成するために使用される関数は、常に同じ形式になります。

```cpp
NTSTATUS CreateMyObject(
   OUT PUNKNOWN  *Unknown,
   IN REFGUID ClassId,
   IN PUNKNOWN OuterUnknown OPTIONAL,
   IN POOL_TYPE PoolType
 );
```

### <a name="span-idparametersspanspan-idparametersspanparameters"></a><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ

<span id="Unknown"></span><span id="unknown"></span><span id="UNKNOWN"></span>*知ら*  
**IUnknown**インターフェイスへのポインターへのポインター。 関数は、新しく作成されたオブジェクトへの参照を*Unknown*を通じて出力します。

<span id="ClassId"></span><span id="classid"></span><span id="CLASSID"></span>*ClassId*  
参照渡しで渡されるクラス GUID を指定します。 このパラメーターは、関数が複数のクラスのオブジェクトを作成する場合にのみ使用されます。 それ以外の場合は、 **NULL**に設定されます。

<span id="OuterUnknown"></span><span id="outerunknown"></span><span id="OUTERUNKNOWN"></span>*OuterUnknown*  
新しいオブジェクトを集計するための**IUnknown**インターフェイスを指定します。 このパラメーターを**NULL**に設定すると、集計が不要であることを示すことができます。

<span id="PoolType"></span><span id="pooltype"></span><span id="POOLTYPE"></span>*PoolType*  
オブジェクトが割り当てられるメモリプールの種類を指定します (「[**プール\_の種類**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_pool_type)」を参照してください)。

最初の3つのパラメーターは、COM **CoCreateInstance**関数のパラメーターと同じです。 この型の作成関数の例については、Microsoft Windows Driver Kit (WDK) の Fmsynth sample audio driver の**CreateMiniportMidiFM**関数を参照してください。

もう1つの規則として、クラスの新しい*Xxx*関数を指定します。 このような関数を使用すると、次の例に示すように、オブジェクトのインスタンス化 (作成と初期化) を簡単に行うことができます。

```cpp
NTSTATUS NewMyObject(
 OUT PMYINTERFACE  *InterfacePointer,
 IN PUNKNOWN  OuterUnknown OPTIONAL,
 IN POOL_TYPE  PoolType,
  // ...more parameters
 );
```

NewMyObject 関数は、オブジェクトを作成して初期化した後、ポインターをインターフェイスに渡します。 初期化パラメーターはクラス固有であるため、は新しい*Xxx*関数のプロトタイプです。 新しい*Xxx*関数を使用すると、オブジェクトのコンストラクターに簡単にアクセスできます。

この型の新しい*Xxx*関数の例については、「 [**PcNewDmaChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewdmachannel)」を参照してください。

 

 




