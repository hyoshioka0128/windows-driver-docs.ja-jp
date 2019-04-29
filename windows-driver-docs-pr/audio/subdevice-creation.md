---
title: サブデバイスの作成
description: サブデバイスの作成
ms.assetid: e4ba1209-adc6-48c3-9633-247e9e3849bc
keywords:
- オーディオ アダプター WDK、サブデバイス
- アダプターのドライバー WDK のオーディオ、サブデバイス
- サブデバイス WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0171b629b3a5978cd90b72fd2f617e0f6f1697c8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328601"
---
# <a name="subdevice-creation"></a>サブデバイスの作成


## <span id="subdevice_creation"></span><span id="SUBDEVICE_CREATION"></span>


用語*サブデバイス*次の表に記載されている 4 つのコンポーネントのバインディングを記述するために使用します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Component</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ミニポート オブジェクト</p></td>
<td align="left"><p>ミニポート ドライバーの IMiniport を公開するオブジェクトを<em>Xxx</em>インターフェイス</p></td>
</tr>
<tr class="even">
<td align="left"><p>ポート オブジェクト</p></td>
<td align="left"><p>ポート ドライバーの IPort を公開するオブジェクトを<em>Xxx</em>インターフェイス</p></td>
</tr>
<tr class="odd">
<td align="left"><p>リソース リスト オブジェクト</p></td>
<td align="left"><p>サブデバイスに割り当てられているアダプターのドライバー リソースの一覧を格納するオブジェクト</p></td>
</tr>
<tr class="even">
<td align="left"><p>参照文字列</p></td>
<td align="left"><p>フィルターの作成中に、サブデバイスを指定するデバイスのパス名に追加の名前</p></td>
</tr>
</tbody>
</table>

 

サブデバイスの IMiniport*Xxx*と IPort*Xxx*基底インターフェイスから継承するインターフェイス[IMiniport](https://msdn.microsoft.com/library/windows/hardware/ff536698)と[IPort](https://msdn.microsoft.com/library/windows/hardware/ff536842)、それぞれします。

PortCls システム ドライバーでは、ポート ドライバーとミニポート ドライバーが区別されません。 システムによって生成された要求を処理できるインターフェイスで、ポート オブジェクトなどのオブジェクトだけが必要です。

同様に、PortCls 直接に関係のないリソースを管理します。 のみ、リソースの一覧に、要求ハンドラー (ポート ドライバー) をバインドする必要があります。 アダプターのドライバーは、ポート、ミニポート、およびリスト オブジェクトのリソースをまとめてバインドします。

次のコード例では、アダプターのドライバーがこれらのアクションを実行する方法を示します。

```cpp
  //
  // Instantiate the port by calling a function supplied by PortCls.
  //
  PPORT    port;
  NTSTATUS ntStatus = PcNewPort(&port, PortClassId);

  if (NT_SUCCESS(ntStatus))
  {
      PUNKNOWN miniport;
      //
      // Create the miniport object.
      //
      if (MiniportCreate)   // a function to create a proprietary miniport
      {
          ntStatus = MiniportCreate(&miniport,
                                    MiniportClassId, NULL, NonPagedPool);
      }
      else   // Ask PortCls for one of its built-in miniports.
      {
          ntStatus = PcNewMiniport((PMINIPORT*)&miniport,
                                   MiniportClassId);
      }

      if (NT_SUCCESS(ntStatus))
      {
          //
          // Bind the port, miniport, and resources.
          //
          ntStatus = port->Init(DeviceObject,
                                Irp, miniport, UnknownAdapter, ResourceList);
          if (NT_SUCCESS(ntStatus))
          {
              //
              // Hand the port driver and the reference
              // string to PortCls.
              //
              ntStatus = PcRegisterSubdevice(DeviceObject,
                                             Name, port);
          }

          //
          // We no longer need to reference the miniport driver.
          // Either the port driver now references it,
          // or binding failed and it should be deleted.
          //
          miniport->Release();
      }

      //
      // Release the reference that existed when PcNewPort() gave us
      // the pointer in the first place. This reference must be released
      // regardless of whether the binding of the port and miniport
      // drivers succeeded.
      //
      port->Release();
  }
```

PortCls 関数の詳細については、上記のコード例の呼び出し、に対するを参照してください[ **PcNewPort**](https://msdn.microsoft.com/library/windows/hardware/ff537715)、 [ **PcNewMiniport**](https://msdn.microsoft.com/library/windows/hardware/ff537714)、および。[**PcRegisterSubdevice**](https://msdn.microsoft.com/library/windows/hardware/ff537731)します。

 

 




