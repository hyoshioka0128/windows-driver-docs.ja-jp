---
title: コンピューターのハードウェア ID の指定
description: コンピューターのハードウェア ID の指定
ms.assetid: af0dbfc4-747c-4e16-a3ed-678df0e07757
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d72d987afa5f0358d16a766f13ffe77ab2791149
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369426"
---
#  <a name="specifying-hardware-ids-for-a-computer"></a>コンピューターのハードウェア ID の指定

デバイスとプリンターとコンピューターを認識する[デバイス コンテナー](container-ids.md)します。 使用して、コンピューターをデバイス メタデータ パッケージ内で識別する結果として、 [ **HardwareID** ](https://msdn.microsoft.com/library/windows/hardware/ff546114)一意を指定する XML 要素[ハードウェア ID](hardware-ids.md)値。  (コンピューターのハードウェア ID、または CHID とも呼ばれます)、コンピューターのハードウェア ID 値は、System Management BIOS (SMBIOS) フィールドのデータの組み合わせを指定できます。

異なり[ハードウェア Id](hardware-ids.md)他のデバイスのコンテナーでは、コンピューターのハードウェア ID が Windows によって生成、システムが起動するたびにします。 Windows Driver Kit (WDK) での Windows 7、Windows 8 および Windows 8.1 に含まれている ComputerHardwareIds ツール (ComputerHardwareIDs.exe) を実行して、コンピューターのハードウェア Id を生成できます。 ComputerHardwareIds ツールには Windows 10 以降のソフトウェア開発キット (SDK) が含まれています。

ComputerHardwareIds ツールでは、フィールド、システムの System Management BIOS (SMBIOS) からの情報に基づいているコンピューターのハードウェア Id のセットを生成します。 次の表では、これらの SMBIOS フィールドについて説明します。

|フィールド名|構造体の名前とタイプ|SMBIOS 仕様のバージョン|Offset|長さ|値|説明|
|--- |--- |--- |--- |--- |--- |--- |
|製造元|システム情報 (タイプ 1)|2.0+|04h|BYTE|STRING|dmiStrucBuffer 配列内の、NULL で終了する文字列のインデックス。 この文字列は、コンピューターの製造元の名前を指定します。|
|Family (ファミリ)|システム情報 (タイプ 1)|2.4+|1Ah|BYTE|STRING|dmiStrucBuffer 配列内の、NULL で終了する文字列のインデックス。 この文字列は、特定のコンピューターが属するファミリを指定します。  ファミリと似ていますが、ハードウェアまたはソフトウェアの観点から同一であるコンピューターのセットを指します。  通常、ファミリは別のコンピューターのモデルは、さまざまな構成と価格のポイントがあるので構成されます。 同じファミリのコンピューターは、多くの場合、ブランドや外観の面で類似した特徴があります。|
|製品名|システム情報 (タイプ 1)|2.0+|05h|BYTE|STRING|dmiStrucBuffer 配列内の、NULL で終了する文字列のインデックス。 この文字列は、コンピューターの製品名を指定します。|
|製造元|BIOS 情報 (タイプ 0)|2.0+|04h|BYTE|STRING|dmiStrucBuffer 配列内の、NULL で終了する文字列のインデックス。 この文字列は、BIOS のベンダーの名前を指定します。|
|BIOS Version (BIOS のバージョン)|BIOS 情報 (タイプ 0)|2.+0|05h|BYTE|STRING|dmiStrucBuffer 配列内の、NULL で終了する文字列のインデックス。 この文字列には、プロセッサ コアと OEM バージョンについての情報を含めることができます。|
|System BIOS Major Release (システム BIOS のメジャー リリース)|BIOS 情報 (タイプ 0)|2.4+|14h|BYTE|状況により異なる。|システム BIOS のメジャー リリース。|
|System BIOS Minor Release (システム BIOS のマイナー リリース)|BIOS 情報 (タイプ 0)|2.4+|15h|BYTE|不定|システム BIOS のマイナー リリース。|
|Enclosure type (筐体の種類)|システム筐体 (タイプ 3)|2.0+|05h|BYTE|不定|システムの筐体またはシャーシの種類。|
|SKU Number (SKU 番号)|SKU の数 (種類 1)|2.4+|19h|BYTE|STRING|販売の特定のコンピューターの構成の id です。|
|ベースボード製造元|製造元 (種類 2)| |04h|BYTE|STRING|Null で終わる文字列の数。 0 ah ベースボード: ボードの種類である、ベースボードの製造元を示す文字列 (マザーボード)。|
|ベースボード製品|製品 (種類 2)| |05h|BYTE|STRING|Null で終わる文字列の数。 0 ah ベースボード: ボードの種類である、ベースボードの製品名を示す文字列 (マザーボード)。|

詳細については、 *dmiStrucBuffer*配列と SMBIOS フィールドを参照してください、 [System Management BIOS (SMBIOS)](https://go.microsoft.com/fwlink/p/?linkid=145867) Distributed Management Task Force (DMTF) web サイトを指定します。

ComputerHardwareIds ツールを実行すると、SMBIOS 情報から固有のハードウェア Id を作成します。 各ハードウェアの ID は、 *GUID*と SMBIOS フィールドから値を連結して作成されます。

次の表では、Windows 7、Windows 8、Windows 8.1、および Windows 10 では、各ハードウェア ID を形成するために使用する SMBIOS フィールドを示します。

**重要な**  各コンピューター HardwareID は、システムのデータに SMBIOS、HardwareID の生成に使用される各 SMBIOS フィールドが設定されている場合にのみ生成されます。

 

| HWID         | Windows 7                                                                                                            |
|--------------|----------------------------------------------------------------------------------------------------------------------|
| HardwareID-0 | 製造元 + ファミリ + 製品名 + ベンダー + BIOS のバージョンとシステム BIOS のメジャー リリース + システム BIOS のマイナー リリース |
| HardwareID-1 | 製造元 + 製品名 + BIOS ベンダー + BIOS のバージョンとシステム BIOS のメジャー リリース + システム BIOS のマイナー リリース     |
| HardwareID-2 | 製造元 + ファミリ + 製品名                                                                                  |
| HardwareID-3 | 製造元 + 製品名                                                                                           |
| HardwareID-4 | 製造元 + ファミリ                                                                                                |
| HardwareID-5 | 製造元 + 筐体の種類                                                                                        |
| HardwareID-6 | 製造元                                                                                                         |

 

| HWID         | Windows 8、Windows 8.1                                                                                                   |
|--------------|--------------------------------------------------------------------------------------------------------------------------|
| HardwareID-0 | 製造元 + ファミリ + 製品名 + SKU 番号 + BIOS ベンダー + BIOS のバージョン + BIOS のメジャー リリース + BIOS のマイナー リリース |
| HardwareID-1 | 製造元 + ファミリ + 製品名 + BIOS ベンダー + BIOS のバージョン + BIOS のメジャー リリース + BIOS のマイナー リリース              |
| HardwareID-2 | 製造元 + 製品名 + BIOS ベンダー + BIOS のバージョン + BIOS のメジャー リリース + BIOS のマイナー リリース                       |
| HardwareID-3 | 製造元 + ファミリ + 製品名 + SKU 番号                                                                         |
| HardwareID-4 | 製造元 + ファミリ + 製品名                                                                                      |
| HardwareID-5 | 製造元 + SKU 番号                                                                                                |
| HardwareID-6 | 製造元 + 製品名                                                                                               |
| HardwareID-7 | 製造元 + ファミリ                                                                                                    |
| HardwareID-8 | 製造元 + 筐体の種類                                                                                            |
| HardwareID-9 | 製造元                                                                                                             |

 

| HWID          | Windows 10                                                                                                               |
|---------------|--------------------------------------------------------------------------------------------------------------------------|
| HardwareID-0  | 製造元 + ファミリ + 製品名 + SKU 番号 + BIOS ベンダー + BIOS のバージョン + BIOS のメジャー リリース + BIOS のマイナー リリース |
| HardwareID-1  | 製造元 + ファミリ + 製品名 + BIOS ベンダー + BIOS のバージョン + BIOS のメジャー リリース + BIOS のマイナー リリース              |
| HardwareID-2  | 製造元 + 製品名 + BIOS ベンダー + BIOS のバージョン + BIOS のメジャー リリース + BIOS のマイナー リリース                       |
| HardwareID-3  | 製造元 + ファミリ + 製品名 + SKU 番号 + ベースボード製造元 + ベースボード製品                           |
| HardwareID-4  | 製造元 + ファミリ + 製品名、SKU 番号                                                                        |
| HardwareID-5  | 製造元 + ファミリ製品名                                                                                     |
| HardwareID-6  | 製造元 + SKU 番号 + ベースボード製造元ベースボード製品                                                   |
| HardwareID-7  | 製造元 + SKU 番号                                                                                                |
| HardwareID-8  | 製造元 + 製品名 + ベースボード製造元ベースボード製品                                                 |
| HardwareID-9  | 製造元と製品名                                                                                              |
| HardwareID-10 | 製造元 + ファミリ + ベースボード製造元ベースボード製品                                                       |
| HardwareID-11 | 製造元 + ファミリ                                                                                                    |
| HardwareID-12 | 製造元 + 筐体の種類                                                                                            |
| HardwareID-13 | 製造元 + ベースボード製造元ベースボード製品                                                                |
| HardwareID-14 | 製造元                                                                                                             |

 

各ハードウェア ID の文字列は、sha-1 ハッシュ アルゴリズムを使用して、GUID に変換されます。

### <a name="using-computer-hardwareids-with-pc-device-metadata-packages"></a>PC デバイス メタデータ パッケージを使用したコンピューター HardwareIDs を使用します。

Windows 7 のシステムでは、強くお勧めを選択するときに、ベンダーが、次を行うことを[ハードウェア ID](hardware-ids.md)として使用する値、 [ **HardwareID** ](https://msdn.microsoft.com/library/windows/hardware/ff546114)の XML 要素の値、コンピューター。

-   使用**HardwareID 3**または**HardwareID 4**デバイス メタデータ パッケージを特定のメーカー、ファミリ、およびモデルを持つコンピューターに一致する場合は、最初の選択肢として。 これにより、コンピューターの最も正確なメタデータを提供する、指定したコンピューターと一致するメタデータ パッケージです。

-   使用**HardwareID 5**、デバイス メタデータ パッケージは、コンピューターのファミリ全体を覆っている場合は、2 つ目の選択肢として。 この場合、コンピューター ファミリが一意とするは、1 つ以上の製品ラインでブランド化されません。

-   使用**HardwareID 6**または**HardwareID 7**デバイス メタデータ パッケージのすべてのコンピューターまたは特定のエンクロージャの種類でそれらのコンピューターの場合は、3 つ目の選択肢として。

**注**  Windows 7 PC デバイスのメタデータを使用しないでください**HardwareID 1**または**HardwareID 2**コンピューターのハードウェア id **ハードウェア ID-1**または**HardwareID 2**は将来使用するために予約されています。

 

**注**  For Windows 8 PC デバイスのメタデータを強くお勧めのベンダーを使用しないこと**HardwareID 1**、 **HardwareID 2**、 **HardwareID 3**コンピューターのハードウェア id **HardwareID 1**、 **HardwareID 2**、 **HardwareID 3**に将来使用するために予約されています。 代わりに、ベンダーが使用できる**HardwareID 4**、 **HardwareID 5**、 **HardwareID 6**、 **HardwareID 7**、 **HardwareID 8**、 **HardwareID 9**、および**HardwareID 10**します。

 

コンピューター デバイスのコンテナーのハードウェア ID であることを指定するには、次の規則を使用します。

-   ハードウェア ID の文字列を区切るため '{0}' と '}' の文字。

-   プレフィックスの追加 'ComputerMetadata\\' ハードウェア ID の文字列の前にします。

例を次に、 [ **HardwareID** ](https://msdn.microsoft.com/library/windows/hardware/ff546114)コンピューターの XML 要素。

```cpp
DOID:ComputerMetadata\{c20d5449-511e-4cb5-902a-a541239322aa}
```

形式の要件の詳細については、 **HardwareID** 、XML 要素を参照してください[ **HardwareID**](https://msdn.microsoft.com/library/windows/hardware/ff546114)します。

## <a name="related-topics"></a>関連トピック


[ワークフローを発行する Windows 10 ドライバー](https://go.microsoft.com/fwlink/p/?LinkId=617374 )

 

 






