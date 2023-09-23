import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

class Bus {
    private int departureTime;
    private int capacity;
    private List<Integer> passengers;

    public Bus(int departureTime, int capacity) {
        this.departureTime = departureTime;
        this.capacity = capacity;
        this.passengers = new ArrayList<>();
    }

    public int getDepartureTime() {
        return departureTime;
    }

    public int getRemainingCapacity() {
        return capacity - passengers.size();
    }

    public boolean canBoard(int passengerArrivalTime) {
        return getRemainingCapacity() > 0 && passengerArrivalTime <= departureTime;
    }

    public void boardPassenger(int passengerArrivalTime) {
        if (canBoard(passengerArrivalTime)) {
            passengers.add(passengerArrivalTime);
        }
    }
}

public class LastBusTime {
    public static int lastPossibleTime(int[] buses, int[] passengers, int capacity) {
        List<Bus> busList = new ArrayList<>();
        for (int busTime : buses) {
            busList.add(new Bus(busTime, capacity));
        }

        List<Integer> passengerList = new ArrayList<>();
        for (int passengerTime : passengers) {
            passengerList.add(passengerTime);
        }
        Collections.sort(passengerList);

        int lastPossibleTime = 0;
        for (int passengerTime : passengerList) {
            for (Bus bus : busList) {
                if (bus.canBoard(passengerTime)) {
                    bus.boardPassenger(passengerTime);
                    lastPossibleTime = passengerTime;
                    break;
                }
            }
        }

        return lastPossibleTime;
    }

    public static void main(String[] args) {
        int[] buses1 = {10, 20};
        int[] passengers1 = {2, 17, 18, 19};
        int capacity1 = 2;
        System.out.println(lastPossibleTime(buses1, passengers1, capacity1)); // Saída: 16

        int[] buses2 = {20, 30, 10};
        int[] passengers2 = {19, 13, 26, 4, 25, 11, 21};
        int capacity2 = 2;
        System.out.println(lastPossibleTime(buses2, passengers2, capacity2)); // Saída: 20
    }
}





