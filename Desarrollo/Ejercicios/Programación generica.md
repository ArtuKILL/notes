## Practica 1

```typescript
interface IMessage {

  show(): void;

}

  

function identity<T, U extends IMessage>(value: T, message: U): T {

  message.show();

  return value;

}

  

class Message implements IMessage {

  private _content: string;

  private _title: string;

  private _date: Date;

  

  protected get content(): string {

    return this._content;

  }

  

  protected get title(): string {

    return this._title;

  }

  

  protected get date(): Date {

    return this._date;

  }

  

  constructor(content: string, title: string) {

    this._content = content;

    this._title = title;

    this._date = new Date();

  }

  

  public show(): void {

    const header = `${this._title} / ${this._date}`;

    const div = [...header].reduce((acc, _) => {

      return acc + "-";

    }, "");

  

    console.log(div);

    console.log(header);

    console.log(div);

    console.log(`${this._content}`);

    console.log("");

  }

}

  

class MessageWithImage extends Message {

  private _image: string;

  

  constructor(content: string, title: string, image: string) {

    super(content, title);

    this._image = image;

  }

  

  override show(): void {

    const header = `${super.title} / ${this.date} / ${this._image}`;

    const div = [...header].reduce((acc, _) => {

      return acc + "-";

    }, "");

    console.log(div);

    console.log(header);

    console.log(div);

    console.log(`${this.content}`);

    console.log("");

  }

}

  

const message: Message = new Message("Hello World", "Hello");

const message2: IMessage = new Message("Hello World", "Hello");

const message3: MessageWithImage = new MessageWithImage(

  "Hola mundo este es mi blog con imagen!!",

  "Imagen",

  "     " //Para ver la imagen usar https://www.nerdfonts.com

);

  

const messageList: Array<IMessage> = [message, message2, message3];

  

let i = 0;

  

messageList.forEach((element) => {

  identity<number, IMessage>(i, element);

  i++;

});

```