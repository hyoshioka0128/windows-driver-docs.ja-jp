---
title: 誤検知を抑制するための _analysis_assume 関数の使用
description: 誤検知を抑制するための _analysis_assume 関数の使用
ms.assetid: eb71a664-ada5-44e3-b75d-b1a7348b115f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 215121b46c1fb8f49f24bb8eece471e62f20f7fa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325421"
---
# <a name="using-the-analysisassume-function-to-suppress-false-defects"></a>使用して、 \_analysis\_False 欠陥を抑制する関数を想定しています


行うことができます Static Driver Verifier (SDV) 追加情報を含む、ドライバーのソース コードを検証中に false 欠陥のレポートを抑制することができます。 False の欠陥は、SDV は、見かけ上の規則違反を報告したときに、ドライバーが正常に機能するような状況で発生します。

SDV は、この追加情報を提供するには、使用、  **\_ \_analysis\_想定**関数。 関数は、次の構文を持ちます。

```
__analysis_assume( expression ) 
```

場所*式*に評価されると見なされますが、任意の式**true**します。

SDV では、によって表される条件はこの関数を使用するときに、*式*は**true**時点で、  **\_ \_analysis\_想定**関数が表示されます。 **\_ \_Analysis\_想定**関数は静的分析ツールでのみ使用されます。 関数は、コンパイラによって無視されます。

使用する場合 **\_\_分析\_と仮定**は非常に重要であることを行っているという前提の有効性の。 判明した場合を想定は**false**、今すぐ または今後、するが true の欠陥を抑制している可能性があります。 使用している理由を説明するコードには常にコメントを追加することをお勧め、  **\_ \_analysis\_想定**関数。 前提の理由を記述することはできません、障害を抑制しないでください。

追加する必要があります、  **\_ \_analysis\_と仮定**必要に応じて機能を非表示にしても問題ありません false の欠陥を見つける場合にします。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

次のコード例、KMDF ルール[RequestCompletedLocal](https://msdn.microsoft.com/library/windows/hardware/ff551609)欠陥を報告します。 擬似欠陥は、SDV を正しく解釈できないため、これは、**切り替える**ステートメントと、その結果を入力していない分岐で、要求が完了した後します。

この**切り替える**ステートメントでは、6 つの可能な場合があります。 ドライバーがドライバーが、分岐のいずれかに実行することは間違いなく、6 つの IOCTL コードを定義します。 分岐のいずれかが実行された場合、要求が正常に完了します。

```
VOID
PortIOEvtIoDeviceControl(
      __in WDFQUEUE     Queue,
      __in WDFREQUEST   Request,
      __in size_t       OutputBufferLength,
  __in size_t       InputBufferLength,
  __in ULONG        IoControlCode
     )
 
     PDEVICE_CONTEXT devContext = NULL;
     WDFDEVICE device;

     PAGED_CODE();
 
     device = WdfIoQueueGetDevice(Queue);
 
     devContext = PortIOGetDeviceContext(device);
 
     switch(IoControlCode)
         case IOCTL_GPD_READ_PORT_UCHAR:
         case IOCTL_GPD_READ_PORT_USHORT:
         case IOCTL_GPD_READ_PORT_ULONG:
             PortIOIoctlReadPort(devContext,
                                 Request,
                                 OutputBufferLength,
                                 InputBufferLength,
                                 IoControlCode);
             break;

 
         case IOCTL_GPD_WRITE_PORT_UCHAR:
         case IOCTL_GPD_WRITE_PORT_USHORT:
         case IOCTL_GPD_WRITE_PORT_ULONG:    
             PortIOIoctlWritePort(devContext,
                                  Request,
                                  OutputBufferLength,
                                  InputBufferLength,
                                  IoControlCode);
             break;
 
     }
 
}
```

擬似欠陥を安全に抑制するのには、使用、  **\_ \_analysis\_想定**ことを指定する関数、 *IoControlCode* Ioctl のいずれかを指定することが保証されますドライバーが定義されています。

```
VOID
PortIOEvtIoDeviceControl(
      __in WDFQUEUE     Queue,
      __in WDFREQUEST   Request,
      __in size_t       OutputBufferLength,
      __in size_t       InputBufferLength,
      __in ULONG        IoControlCode
     )
 
     PDEVICE_CONTEXT devContext = NULL;
     WDFDEVICE device;

     PAGED_CODE();
 
     device = WdfIoQueueGetDevice(Queue);
 
     devContext = PortIOGetDeviceContext(device);

/* Use __analysis_assume to suppress a false defect for the SDV RequestCompletedLocal rule. 
There are only 6 possible IOCTLs for IoControlCode; each case is covered in the switch statement.
*/

 __analysis_assume( IoControlCode == IOCTL_GPD_READ_PORT_UCHAR || \
                       IoControlCode == IOCTL_GPD_READ_PORT_USHORT|| \
                       IoControlCode == IOCTL_GPD_READ_PORT_ULONG || \
                       IoControlCode == IOCTL_GPD_WRITE_PORT_UCHAR|| \
                       IoControlCode == IOCTL_GPD_WRITE_PORT_USHORT|| \
                       IoControlCode == IOCTL_GPD_WRITE_PORT_ULONG);

     switch(IoControlCode)
         case IOCTL_GPD_READ_PORT_UCHAR:
         case IOCTL_GPD_READ_PORT_USHORT:
         case IOCTL_GPD_READ_PORT_ULONG:
             PortIOIoctlReadPort(devContext,
                                 Request,
                                 OutputBufferLength,
                                 InputBufferLength,
                                 IoControlCode);
             break;

 
         case IOCTL_GPD_WRITE_PORT_UCHAR:
         case IOCTL_GPD_WRITE_PORT_USHORT:
         case IOCTL_GPD_WRITE_PORT_ULONG:    
             PortIOIoctlWritePort(devContext,
                                  Request,
                                  OutputBufferLength,
                                  InputBufferLength,
                                  IoControlCode);
             break;
 
     }
 
}
```

使用する方法のもう 1 つの例については **\_ \_analysis\_前提としています**で使用されているコード例を参照してください[Using \_ \_sdv\_保存。\_要求と\_ \_sdv\_取得\_遅延プロシージャ呼び出しの要求](using---sdv-save-request-and---sdv-retrieve-request-for-deferred-proce.md)します。 例では、使用する方法を示します **\_ \_sdv\_保存\_要求**と **\_ \_sdv\_取得\_要求**Dpc (作業項目やタイマー) にします。 **\_ \_Analysis\_想定**招く可能性がある場合は false の欠陥を抑制する関数を使用します。

 

 





