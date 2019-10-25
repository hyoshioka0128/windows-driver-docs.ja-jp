---
title: サブデバイスの作成
description: サブデバイスの作成
ms.assetid: e4ba1209-adc6-48c3-9633-247e9e3849bc
keywords:
- オーディオアダプター WDK、サブデバイス
- アダプタードライバー WDK オーディオ、サブデバイス
- サブデバイス WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b66c8b9d7c71316c78d3cfec59ab68780c68b36b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832351"
---
# <a name="subdevice-creation"></a>サブデバイスの作成


## <span id="subdevice_creation"></span><span id="SUBDEVICE_CREATION"></span>


*サブデバイス*という用語は、次の表に示す4つのコンポーネントのバインドを記述するために使用されます。

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
<td align="left"><p>ミニポートオブジェクト</p></td>
<td align="left"><p>ミニポートドライバーの IMiniport<em>Xxx</em>インターフェイスを公開するオブジェクト</p></td>
</tr>
<tr class="even">
<td align="left"><p>ポートオブジェクト</p></td>
<td align="left"><p>ポートドライバーの IPort<em>Xxx</em>インターフェイスを公開するオブジェクト。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>リソースリストオブジェクト</p></td>
<td align="left"><p>サブデバイスに割り当てられているアダプタードライバーリソースのリストを格納しているオブジェクト。</p></td>
</tr>
<tr class="even">
<td align="left"><p>参照文字列</p></td>
<td align="left"><p>フィルターの作成時にサブデバイスを指定するためにデバイスパス名に追加された名前</p></td>
</tr>
</tbody>
</table>

 

サブデバイスの IMiniport*Xxx*インターフェイスと IPort*xxx*インターフェイスは、それぞれ基本インターフェイス[IMiniport](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiport)と[IPort](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iport)を継承します。

PortCls システムドライバーは、ポートドライバーとミニポートドライバーを区別しません。 これには、ポートオブジェクトなどのオブジェクトと、システムによって生成された要求を処理できるインターフェイスが必要です。

同様に、PortCls はリソースの管理に直接は関与しません。 要求ハンドラー (ポートドライバー) をリソースリストにバインドするだけで済みます。 アダプタードライバーは、ポート、ミニポート、およびリソースリストオブジェクトをまとめてバインドします。

次のコード例は、アダプタードライバーがこれらのアクションを実行する方法を示しています。

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

前のコード例の PortCls 関数呼び出しの詳細については、「 [**Pcnewport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewport)、 [**pcnewport ポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewminiport)、および[**Pcregiのサブデバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregistersubdevice)」を参照してください。

 

 




