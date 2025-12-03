package frc.robot;

import edu.wpi.first.wpilibj.TimedRobot;
import edu.wpi.first.wpilibj.Joystick;
import edu.wpi.first.wpilibj.drive.DifferentialDrive;

// REV SparkMax imports
import com.revrobotics.spark.SparkMax;
import com.revrobotics.spark.SparkLowLevel.MotorType;

public class Robot extends TimedRobot {

  // 4 SparkMax controllers
  private SparkMax m_leftFront;
  private SparkMax m_leftRear;
  private SparkMax m_rightFront;
  private SparkMax m_rightRear;

  private DifferentialDrive m_drive;
  private Joystick m_stick;

  @Override
  public void robotInit() {
    // CAN IDs you listed:
    // front left = 3
    // back left  = 2
    // front right = 5
    // back right = 4

    m_leftFront = new SparkMax(3, MotorType.kBrushed);
    m_leftRear  = new SparkMax(2, MotorType.kBrushed);

    m_rightFront = new SparkMax(5, MotorType.kBrushed);
    m_rightRear  = new SparkMax(4, MotorType.kBrushed);

    // INVERSION (kept same structure, only touched motor assignments)
    m_leftFront.setInverted(false);
    m_leftRear.setInverted(false);

    m_rightFront.setInverted(true);
    m_rightRear.setInverted(false);

    m_drive = new DifferentialDrive(m_leftFront, m_rightFront);

    m_stick = new Joystick(0);
  }

  @Override
  public void teleopPeriodic() {
    double forward = -m_stick.getY();
    double turn = m_stick.getX();

    m_drive.arcadeDrive(forward, turn);
  }
}
