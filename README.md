// # FANTASY-LEAGUE-APPLICATION
package com.fantasyleague;

import java.util.*;

class Player {
    String name;
    String team;
    int points;

    Player(String name, String team, int points) {
        this.name = name;
        this.team = team;
        this.points = points;
    }

    public String toString() {
        return name + " (" + team + ") - Points: " + points;
    }
}

public class FantasyLeagueApp {
    private static final List<Player> availablePlayers = new ArrayList<>();
    private static final List<Player> selectedTeam = new ArrayList<>();
    private static final int MAX_TEAM_SIZE = 5;

    public static void main(String[] args) {
        initPlayers();
        Scanner scanner = new Scanner(System.in);
        boolean running = true;

        while (running) {
            System.out.println("\nFantasy League App - Dream11 Clone");
            System.out.println("1. View Available Players");
            System.out.println("2. Select Player");
            System.out.println("3. View My Team");
            System.out.println("4. Calculate Total Points");
            System.out.println("5. Exit");
            System.out.print("Choose an option: ");

            int choice = scanner.nextInt();
            scanner.nextLine();

            switch (choice) {
                case 1 -> displayAvailablePlayers();
                case 2 -> selectPlayer(scanner);
                case 3 -> displayTeam();
                case 4 -> calculatePoints();
                case 5 -> {
                    System.out.println("Exiting Fantasy League App. Good luck!");
                    running = false;
                }
                default -> System.out.println("Invalid option. Try again.");
            }
        }
    }

    private static void initPlayers() {
        availablePlayers.add(new Player("Virat Kohli", "RCB", 85));
        availablePlayers.add(new Player("MS Dhoni", "CSK", 75));
        availablePlayers.add(new Player("Rohit Sharma", "MI", 90));
        availablePlayers.add(new Player("KL Rahul", "LSG", 80));
        availablePlayers.add(new Player("Hardik Pandya", "MI", 70));
        availablePlayers.add(new Player("Shubman Gill", "GT", 88));
    }

    private static void displayAvailablePlayers() {
        System.out.println("\nAvailable Players:");
        for (int i = 0; i < availablePlayers.size(); i++) {
            System.out.println((i + 1) + ". " + availablePlayers.get(i));
        }
    }

    private static void selectPlayer(Scanner scanner) {
        if (selectedTeam.size() >= MAX_TEAM_SIZE) {
            System.out.println("Team is full. Cannot select more than " + MAX_TEAM_SIZE + " players.");
            return;
        }
        displayAvailablePlayers();
        System.out.print("Enter player number to select: ");
        int index = scanner.nextInt() - 1;
        scanner.nextLine();

        if (index >= 0 && index < availablePlayers.size()) {
            Player selected = availablePlayers.get(index);
            if (selectedTeam.contains(selected)) {
                System.out.println("Player already selected.");
            } else {
                selectedTeam.add(selected);
                System.out.println("Player added to your team: " + selected.name);
            }
        } else {
            System.out.println("Invalid player number.");
        }
    }

    private static void displayTeam() {
        System.out.println("\nYour Fantasy Team:");
        for (Player player : selectedTeam) {
            System.out.println(player);
        }
    }

    private static void calculatePoints() {
        int total = selectedTeam.stream().mapToInt(p -> p.points).sum();
        System.out.println("\nTotal Fantasy Points: " + total);
    }
}
