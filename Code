# Command-Design-Pattern

package com.company;

import java.io.PrintStream;
import java.util.Stack;

import static com.company.CommandDesignPattern.so;

public class CommandDesignPattern {
    static PrintStream so = System.out;


    public static void runSimpleRemoteControl() {
        SimpleRemoteControl remote = new SimpleRemoteControl();
        Light light = new Light("Kitchen");
        LightOnCommand lightOn = new LightOnCommand(light);
        LightOffCommand lightOff = new LightOffCommand(light);

        remote.setCommand(lightOn);
        remote.buttonWasPressed();

        remote.setCommand(lightOff);
        remote.buttonWasPressed();
    }

    public static void runRemoteControl() {
        RemoteControl rc = new RemoteControl();

        Light lrLight = new Light("Living room");
        Light macroLight = new Light("Party room");
        Light kitchenLight = new Light("Kitchen");
        CeilingFan ceilingFan = new CeilingFan("Living room");
        CeilingFan macroceilingFan = new CeilingFan("Party room");
        GarageDoor garageDoor = new GarageDoor("Garage door");
        Stereo stereo = new Stereo("Living room");
        Stereo macroStereo = new Stereo("Party room");
        Tv tv = new Tv("TV");
        HotTub hotTub = new HotTub("Hot Tub");

        LightOnCommand macroLightOn = new LightOnCommand(macroLight);
        LightOffCommand macroLightOff = new LightOffCommand(macroLight);

        LightOnCommand lrLightOn = new LightOnCommand(lrLight);
        LightOffCommand lrLightOff = new LightOffCommand(lrLight);

        LightOnCommand kitchenLightOn = new LightOnCommand(kitchenLight);
        LightOffCommand kitchenLightOff = new LightOffCommand(kitchenLight);

        CeilingFanHighCommand macroceilingFanHigh = new CeilingFanHighCommand(macroceilingFan);
        CeilingFanMediumCommand macroceilingFanMedium = new CeilingFanMediumCommand(macroceilingFan);
        CeilingFanLowCommand macroceilingFanLow = new CeilingFanLowCommand(macroceilingFan);
        CeilingFanOffCommand macroceilingFanOff = new CeilingFanOffCommand(macroceilingFan);

        CeilingFanHighCommand ceilingFanHigh = new CeilingFanHighCommand(ceilingFan);
        CeilingFanMediumCommand ceilingFanMedium = new CeilingFanMediumCommand(ceilingFan);
        CeilingFanLowCommand ceilingFanLow = new CeilingFanLowCommand(ceilingFan);
        CeilingFanOffCommand ceilingFanOff = new CeilingFanOffCommand(ceilingFan);

        GarageDoorUpCommand garageDoorUp = new GarageDoorUpCommand(garageDoor);
        GarageDoorDownCommand garageDoorDown = new GarageDoorDownCommand(garageDoor);

        StereoOnWithCDCommand macrostereoOnWithCD = new StereoOnWithCDCommand(macroStereo);
        StereoOffCommand macrostereoOff = new StereoOffCommand(macroStereo);

        StereoOnWithCDCommand stereoOnWithCD = new StereoOnWithCDCommand(stereo);
        StereoOffCommand stereoOff = new StereoOffCommand(stereo);

        TvOnWithChannelCommand tvOnWithChannel = new TvOnWithChannelCommand(tv);
        TvOffCommand tvOff = new TvOffCommand(tv);

        HotTubOnWithTempCommand hotTubOnWithTemp = new HotTubOnWithTempCommand(hotTub);
        HotTubOffCommand hotTubOff = new HotTubOffCommand(hotTub);

        Command[] partyOn = { macroLightOn, macroceilingFanHigh, macrostereoOnWithCD, tvOnWithChannel, hotTubOnWithTemp};
        Command[] partyOff = { macroLightOff, macroceilingFanOff, macrostereoOff, tvOff, hotTubOff};

        MacroCommand partyOnMacro = new MacroCommand(partyOn);
        MacroCommand partyOffMacro = new MacroCommand(partyOff);


        rc.setCommand(0, lrLightOn, lrLightOff);
        rc.setCommand(1, kitchenLightOn, kitchenLightOff);
        rc.setCommand(2, stereoOnWithCD, stereoOff);
        rc.setCommand(3, garageDoorUp, garageDoorDown);
        rc.setCommand(4, ceilingFanHigh, ceilingFanOff);
        rc.setCommand(5, ceilingFanMedium, ceilingFanOff);
        rc.setCommand(6, ceilingFanLow, ceilingFanOff);
        rc.setCommand(7, tvOnWithChannel, tvOff);
        rc.setCommand(8, hotTubOnWithTemp, hotTubOff);
        rc.setCommand(0, partyOnMacro, partyOffMacro);


        so.println(rc);

        for (int i = 0; i <= 8; ++i) {
            rc.onButtonWasPushed(i);

        }  // simplifies code
        so.println("\n");
        rc.undoButtonWasPushed();
        rc.undoButtonWasPushed();
        rc.undoButtonWasPushed();

        so.println("\nMacro On\n");
        rc.onButtonWasPushed(0);
        so.println("\nMacro Off\n");
        rc.offButtonWasPushed(0);
    }


    public static void main(String[] args) {
        so.println("Command Design Pattern");

//    runSimpleRemoteControl();
        runRemoteControl();
    }
}
class SimpleRemoteControl {
    private Command command;
    public void setCommand(Command command) { this.command = command; }
    public void buttonWasPressed() { command.execute(); }
}



class RemoteControl {
    Command[] onCommands;
    Command[] offCommands;
    Command undoCommand;
    Stack<Command> undoCommands, redoCommands;

    public RemoteControl() {
        onCommands = new Command[9];
        offCommands = new Command[9];

        undoCommands = new Stack<Command>();
        redoCommands = new Stack<Command>();

        Command noCommand = new NoCommand();
        for (int i = 0; i < 9; ++i) {
            onCommands[i] = offCommands[i] = noCommand;
        }
        undoCommand = noCommand;
    }

    public void setCommand(int slot, Command onCommand, Command offCommand) {
        onCommands[slot] = onCommand;
        offCommands[slot] = offCommand;
    }

    public void onButtonWasPushed(int slot)  {
        undoCommand = onCommands[slot];
        undoCommand.execute();
        undoCommands.push(undoCommand);
    }
    public void offButtonWasPushed(int slot) {
        undoCommand = offCommands[slot];
        undoCommand.execute();
        undoCommands.push(undoCommand);
    }
    public void onThenOffButtonWasPushed(int slot) {
        onButtonWasPushed(slot);
        offButtonWasPushed(slot);
        so.println(" ");
    }
    public void undoButtonWasPushed() {
        undoCommand.undo();
        Command command = undoCommands.pop();
        redoCommands.push(command);
    }

    public void redoButtonWasPushed() {
        Command command = redoCommands.pop();
        command.execute();
        undoCommands.push(command);
    }
    public String toString() {
        StringBuffer sb = new StringBuffer();

        sb.append("\n Remote Control \n");
        for (int i = 0; i < onCommands.length; ++i) {
            sb.append(String.format("[slot %d] %34s     %s\n", i,
                    onCommands[i].getClass().getName(), offCommands[i].getClass().getName()));
        }
        return sb.toString();
    }
}

abstract class Named {
    private String name;
    public Named(String name) { this.name = name; }
    public String getName() { return name; }
    public void setName(String name) { this.name = name; }
}

class Light extends Named {
    public Light(String name) { super(name); }

    public void on()  { so.println(getName() + " light is on.");  }
    public void off() { so.println(getName() + " light is off."); }
}

enum FAN_SPEED { OFF, LOW, MEDIUM, HIGH };

class CeilingFan extends Named {
    private FAN_SPEED speed;

    public CeilingFan(String name) {
        super(name);
        speed = FAN_SPEED.OFF;
    }
    public void high()   { speed = FAN_SPEED.HIGH;    show(); }
    public void medium() { speed = FAN_SPEED.MEDIUM;  show(); }
    public void low()    { speed = FAN_SPEED.LOW;     show(); }
    public FAN_SPEED getSpeed() { return speed; }

    public String toString() { return String.format("Fan %s is on speed %d", getName(), speed); }
    public void show() { so.println(getName() + " ceiling fan is on speed: " + speed); }
    public void on()  {
        medium();
        so.println(getName() + " ceiling fan is on speed: " + speed);
    }
    public void off() { speed = FAN_SPEED.OFF;  show(); }
}

class GarageDoor extends Named {
    public GarageDoor(String name) { super(name); }
    //public String getName() { return "Garage door"; }

    public void up()  { so.println(getName() + " is up.");  }
    public void down() { so.println(getName() + " is down."); }
}

class Stereo extends Named {
    public Stereo(String name) { super(name); }

    public void onWithCD()  { so.println(getName() + " stereo cd is on.");  }
    public void off() { so.println(getName() + " stereo is off."); }
}

class Tv extends Named {
    public Tv(String name) { super(name); }

    public void onWithChannel() { so.println(getName() + " channel is on."); }
    public void off() { so.println(getName() + " is off."); }
}

class HotTub extends Named {
    public HotTub(String name) { super(name); }

    public void onWithTemp() { so.println(getName() + " is on."); }
    public void off() { so.println(getName() + " is off."); }

}

interface Command {
    void execute();
    void undo();
}

class NoCommand implements Command {
    public void execute() { }
    public void undo() { }
}

class LightOnCommand implements Command {
    Light light;

    public LightOnCommand(Light light) { this.light = light; }
    public void execute() { light.on(); }
    public void undo() { light.off();}
}

class LightOffCommand implements Command {
    Light light;

    public LightOffCommand(Light light) { this.light = light; }
    public void execute() { light.off(); }
    public void undo() { light.on(); }
}

class MacroCommand implements Command {
    Command[] commands;
    public MacroCommand(Command[] commands) {
        this.commands = commands;
    }
    public void execute() {
        for (int i = 0; i < commands.length; i++) {
            commands[i].execute();
        }
    }
    public void undo() {
        for (int i = 0; i < commands.length; i++) {
            commands[i].undo();
        }
    }
}

abstract class CeilingFanCommand implements Command {
    CeilingFan fan;
    FAN_SPEED prevSpeed;

    public CeilingFanCommand(CeilingFan fan) {
        this.fan = fan;
        prevSpeed = FAN_SPEED.OFF;
    }
    public abstract void execute();

    public void undo() {
        switch(prevSpeed) {
            case HIGH:    fan.high();    break;
            case MEDIUM:  fan.medium();  break;
            case LOW:     fan.low();     break;
            case OFF:     fan.off();     break;
        }
    }
}

class CeilingFanHighCommand extends CeilingFanCommand {
    public CeilingFanHighCommand(CeilingFan fan) { super(fan); }
    public void execute() {
        prevSpeed = fan.getSpeed();
        fan.high();
    }
}
class CeilingFanMediumCommand extends CeilingFanCommand {
    public CeilingFanMediumCommand(CeilingFan fan) { super(fan); }
    public void execute() {
        prevSpeed = fan.getSpeed();
        fan.medium();
    }
}
class CeilingFanLowCommand extends CeilingFanCommand {
    public CeilingFanLowCommand(CeilingFan fan) { super(fan); }
    public void execute() {
        prevSpeed = fan.getSpeed();
        fan.low();
    }
}
class CeilingFanOffCommand extends CeilingFanCommand {
    public CeilingFanOffCommand(CeilingFan fan) { super(fan); }
    public void execute() {
        prevSpeed = fan.getSpeed();
        fan.off();
    }
}

class GarageDoorUpCommand implements Command {
    GarageDoor garageDoor;

    public GarageDoorUpCommand(GarageDoor door) { this.garageDoor = door; }
    public void execute() { garageDoor.up(); }
    public void undo() { garageDoor.down(); }
}

class GarageDoorDownCommand implements Command {
    GarageDoor garageDoor;

    public GarageDoorDownCommand(GarageDoor door) { this.garageDoor = door; }
    public void execute() { garageDoor.down(); }
    public void undo() { garageDoor.up(); }
}

class StereoOnWithCDCommand implements Command {
    Stereo stereo;

    public StereoOnWithCDCommand(Stereo stereo) { this.stereo = stereo; }
    public void execute() { stereo.onWithCD(); }
    public void undo() { stereo.off(); }
}

class StereoOffCommand implements Command {
    Stereo stereo;
    public StereoOffCommand(Stereo stereo) { this.stereo = stereo; }
    public void execute() { stereo.off(); }
    public void undo() {stereo.onWithCD(); }
}

class TvOnWithChannelCommand implements Command {
    Tv tv;
    public TvOnWithChannelCommand(Tv tv) { this.tv = tv; }
    public void execute() { tv.onWithChannel(); }
    public void undo() { tv.off(); }
}

class TvOffCommand implements Command {
    Tv tv;
    public TvOffCommand(Tv tv) { this.tv = tv; }
    public void execute() { tv.off(); }
    public void undo() { tv.onWithChannel(); }
}

class HotTubOnWithTempCommand implements Command {
    HotTub hotTub;
    public HotTubOnWithTempCommand(HotTub hotTub) { this.hotTub = hotTub; }
    public void execute() { hotTub.onWithTemp(); }
    public void undo() { hotTub.off(); }
}

class HotTubOffCommand implements Command {
    HotTub hotTub;
    public HotTubOffCommand(HotTub hotTub) { this.hotTub = hotTub; }
    public void execute() { hotTub.off(); }
    public void undo() { hotTub.onWithTemp(); }
}

/* Output

Command Design Pattern

 Remote Control
[slot 0]           com.company.MacroCommand     com.company.MacroCommand
[slot 1]         com.company.LightOnCommand     com.company.LightOffCommand
[slot 2]  com.company.StereoOnWithCDCommand     com.company.StereoOffCommand
[slot 3]    com.company.GarageDoorUpCommand     com.company.GarageDoorDownCommand
[slot 4]  com.company.CeilingFanHighCommand     com.company.CeilingFanOffCommand
[slot 5] com.company.CeilingFanMediumCommand     com.company.CeilingFanOffCommand
[slot 6]   com.company.CeilingFanLowCommand     com.company.CeilingFanOffCommand
[slot 7] com.company.TvOnWithChannelCommand     com.company.TvOffCommand
[slot 8] com.company.HotTubOnWithTempCommand     com.company.HotTubOffCommand

Party room light is on.
Party room ceiling fan is on speed: HIGH
Party room stereo cd is on.
TV channel is on.
Hot Tub is on.
Kitchen light is on.
Living room stereo cd is on.
Garage door is up.
Living room ceiling fan is on speed: HIGH
Living room ceiling fan is on speed: MEDIUM
Living room ceiling fan is on speed: LOW
TV channel is on.
Hot Tub is on.


Hot Tub is off.
Hot Tub is off.
Hot Tub is off.

Macro On

Party room light is on.
Party room ceiling fan is on speed: HIGH
Party room stereo cd is on.
TV channel is on.
Hot Tub is on.

Macro Off

Party room light is off.
Party room ceiling fan is on speed: OFF
Party room stereo is off.
TV is off.
Hot Tub is off.

 */ 
