---
title: INF InterfaceInstall32 セクション
description: このセクションでは、1つまたは複数の新しいデバイスインターフェイスクラスを作成します。
ms.assetid: 7cd576a7-aa5b-486c-a622-cdcb9e7448b5
keywords:
- INF InterfaceInstall32 セクションデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF InterfaceInstall32 Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: df390106f4f2ecd3246e41072553b6902ad28345
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223284"
---
# <a name="inf-interfaceinstall32-section"></a>INF InterfaceInstall32 セクション


このセクションでは、1つまたは複数の新しい[デバイスインターフェイスクラス](device-interface-classes.md)を作成します。 新しいクラスが作成されると、その後にインストールされたデバイス/ドライバーを、 [**INF *ddinstall*を使用して新しいデバイスインターフェイスクラスをサポートするように登録できます。**](inf-ddinstall-interfaces-section.md)各 INF ファイル内のセクションをインターフェイスするか、 [**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)を呼び出します。

```inf
[InterfaceInstall32]
 
{InterfaceClassGUID}=install-interface-section[,flags]
...
```

## <a name="entries"></a>エントリ


<a href="" id="interfaceclassguid"></a>*InterfaceClassGUID*  
新しくエクスポートされた[デバイスインターフェイスクラス](device-interface-classes.md)を識別する GUID 値を指定します。

インターフェイスクラスのインスタンスを登録するには、このセクションの指定された GUID 値が inf Ddinstall の[**Inf AddInterface ディレクティブ**](inf-addinterface-directive.md)によって参照されている必要があり[**ます。 *DDInstall*インターフェイスセクション**](inf-ddinstall-interfaces-section.md)、または新しくインストールされたデバイスのドライバーは、この GUID を使用して[**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)を呼び出す必要があります。

GUID を作成する方法の詳細については、「[ドライバーでの guid の使用](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-guids-in-drivers)」を参照してください。 システム定義のインターフェイスクラス GUID については、カーネルストリーミングインターフェイスの*Ks*など、適切なヘッダーを参照してください。

<a href="" id="install-interface-section"></a>*install-interface-section*  
この INF 内の他の場所で、場合によっては、システム定義の拡張機能を使用して、INF ライターで定義されたセクションを参照します。

<a href="" id="flags"></a>*示す*  
指定する場合、このエントリは0である必要があります。

<a name="remarks"></a>解説
-------

指定された*InterfaceClassGUID*がシステムにまだインストールされていない場合、そのインターフェイスクラスは対応する<em>ddinstall</em>としてインストールされ**ます。インターフェイス**セクションは、デバイスのインストール中、またはデバイスのドライバーが**IoRegisterDeviceInterface**への最初の呼び出しを行うときに、 [setupapi.log](setupapi.md)関数によって処理されます。

各*インストールインターフェイスセクション*名は、INF ファイル内で一意である必要があります。また、セクション名を定義するための一般的な規則に従う必要があります。 これらの規則の詳細については、「 [INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)」を参照してください。

指定したすべての*インストールインターフェイスセクション*の一般的な形式は次のとおりです。

```inf
[interface-install-section] | 
[interface-install-section.nt] | 
[interface-install-section.ntx86] | 
[interface-install-section.ntia64] | (Windows XP and later versions of Windows)
[interface-install-section.ntamd64] (Windows XP and later versions of Windows)
[interface-install-section.ntarm] (Windows 8 and later versions of Windows)
[interface-install-section.ntarm64] (Windows 10 and later versions of Windows)


 
AddReg=add-registry-section[, add-registry-section] ...
[AddProperty=add-property-section[, add-property-section] ...]  (Windows Vista and later versions of Windows)
[Copyfiles=@filename | file-list-section[, file-list-section] ...]
[DelReg=del-registry-section[, del-registry-section] ...]
[DelProperty=del-property-section[, del-property-section] ...]  (Windows Vista and later versions of Windows)
[BitReg=bit-registry-section[,bit-registry-section]...]
[Delfiles=file-list section[, file-list-section] ...]
[Renfiles=file-list-section[, file-list-section] ...]
[UpdateInis=update-ini-section[,update-ini-section]...]
[UpdateIniFields=update-inifields-section[,update-inifields-section]...]
[Ini2Reg=ini-to-registry-section[,ini-to-registry-section]...]
...
```

*Interface-install*セクションのエントリの詳細については、「 [**INF Ddinstall」セクション**](inf-ddinstall-section.md)を参照してください。

Windows Vista 以降では、interface-install セクションに[**INF AddProperty ディレクティブ**](inf-addproperty-directive.md)を含めることによって、[デバイスインターフェイスクラス](device-interface-classes.md)のプロパティを設定できます。 また、interface-install セクションに[**INF DelProperty ディレクティブ**](inf-delproperty-directive.md)を含めることによって、デバイスインターフェイスクラスのプロパティを削除することもできます。 ただし、 **Addproperty**または**delproperty**ディレクティブは、windows Vista 以降のバージョンの windows オペレーティングシステムに新しく追加されたデバイスインターフェイスクラスのプロパティを変更する場合にのみ使用してください。 Windows Server 2003、Windows XP、または Windows 2000 で導入され、対応するレジストリ値のエントリを持つデバイスインターフェイスクラスのプロパティの場合は、 [**Inf AddReg ディレクティブ**](inf-addreg-directive.md)と[**inf delreg ディレクティブ**](inf-delreg-directive.md)を使用して、デバイスインターフェイスクラスのプロパティを設定および削除する必要があります。 これらのガイドラインは、システム定義のプロパティとカスタムプロパティに適用されます。 **Addproperty**ディレクティブおよび**delproperty**ディレクティブの使用方法の詳細については、「 [INF Addproperty ディレクティブと inf delproperty ディレクティブ](using-the-inf-addproperty-directive-and-the-inf-delproperty-directive.md)の使用」を参照してください。

**AddReg**ディレクティブは、このインターフェイスのインストール時にレジストリにデバイスインターフェイス固有の情報を設定する1つ以上の追加レジストリセクションを参照します。 このような add registry セクションで指定された**Hkr**は **..Deviceclasses\\{**<em>InterfaceClassGUID</em>**}** キー。

このインターフェイスクラスに関するレジストリ情報には、少なくとも新しい[デバイスインターフェイスクラス](device-interface-classes.md)のフレンドリ名と、このインターフェイスを開いて使用するときに上位レベルのコンポーネントが必要とする情報が含まれている必要があります。

また、このような*インストールインターフェイスセクション*では、ここに示した任意のディレクティブを使用して、インターフェイス固有のインストール操作を指定することもできます。

システム定義の**nt**、 **ntx86**、. **ntia64**、. **ntamd64**、. **ntarm**、 **ntarm64**の各拡張機能の使用方法の詳細については、「[複数のプラットフォームおよびオペレーティングシステム用の INF ファイルの作成](creating-inf-files-for-multiple-platforms-and-operating-systems.md)」を参照してください。

## <a name="see-also"></a>関連項目


[**AddProperty**](inf-addproperty-directive.md)

[**AddReg**](inf-addreg-directive.md)

[**BitReg**](inf-bitreg-directive.md)

[**ClassInstall32**](inf-classinstall32-section.md)

[**CopyFiles**](inf-copyfiles-directive.md)

[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall *。インターフェイス**](inf-ddinstall-interfaces-section.md)

[**DelFiles**](inf-delfiles-directive.md)

[**DelProperty**](inf-delproperty-directive.md)

[**DelReg**](inf-delreg-directive.md)

[**Ini2Reg**](inf-ini2reg-directive.md)

[**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)

[**RenFiles**](inf-renfiles-directive.md)

[**UpdateIniFields**](inf-updateinifields-directive.md)

[**UpdateInis**](inf-updateinis-directive.md)

 

 






